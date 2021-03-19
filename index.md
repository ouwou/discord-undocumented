* auto-gen TOC:
{:toc}

If a "(?)" is at the end of a field or type name it means it might be optional or nullable but is not known for sure

### Thread Channels

Drafted [here](https://github.com/discord/discord-api-docs/pull/2693)

Used for ephemeral conversations started from existing channels. Users can join and leave threads. Can also be manually archived and unarchived

#### Create Thread

POST `/channels/{channel.id}/messages/{message.id}/threads`
Creates a new thread starting in a channel attached to the given message. Return value unknown  
JSON parameters:

| Field                 | Type   | Description                                                  |
|-----------------------|--------|--------------------------------------------------------------|
| auto_archive_duration | int    | minutes until the thread should be archived after inactivity |
| name                  | string | name of the thread                                           |
| type                  | int    | thread channel type. see [channel types](#channel-types)     |
|

#### Thread Member

Unknown method `/channels/{thread.id}/thread-members/{user.id}`  
Unknown return. {user.id} may be substituted with @me

#### Thread Member Settings

Unknown method `/channels/{thread.id}/thread-members/@me/settings`  
Unknown return

#### Channel Types
* PUBLIC_THREAD = 11
* PRIVATE_THREAD = 12

#### Message Types
* THREAD_STARTER_MESSAGE = 21

#### Message Flags
* HAS_THREAD = 1 << 5

#### Dispatch events
* THREAD_CREATE
* THREAD_UPDATE
* THREAD_DELETE
* THREAD_LIST_SYNC
* THREAD_MEMBER_UPDATE
* THREAD_MEMBERS_UPDATE
  
Channel objects may contain the field `thread_metadata` as described below:

#### Thread Metadata Object

| Field                 | Type      | Description                                                  |
|-----------------------|-----------|--------------------------------------------------------------|
| archived              | bool(?)   | ?                                                            |
| auto_archive_duration | integer   | minutes until the thread should be archived after inactivity |
| ?archiver_id          | snowflake | the id of the user who archived the thread                   |
| archive_timestamp(?)  | ?         | ?                                                            |
|

Guild objects may also contain the field `threads`, an array, whose structure is currently unknown

<details>
	<summary>show images</summary>
	<img src="media/thread_create.png">
	<img src="media/creating_new_thread.png">
</details>
&nbsp;  

### Stage Channels
  
Stages are a special type of voice channel where members are organized into speakers, audience, and stage moderators. Stage moderators are speakers themselves and can manage the stage including speakers and the audience. The audience listens to the speaker or speakers and can also have the ability to raise their hands in order to request to speak.

#### Channel Types:
* GUILD_STAGE_VOICE = 13

<details>
	<summary>show images</summary>
	<img src="media/stage_channel_list.png">
	<img src="media/stage_channel_perms.png">
	<img src="media/manage_stage_moderators.png">
</details>
&nbsp;  

### Role Member Counts

Retrieves the number of members with each role  
[GitHub issue](https://github.com/discord/discord-api-docs/issues/2610#issuecomment-778985709)

GET `/api/guilds/{guild.id}/roles/member-counts`  
Returns json object where the key is the role ID and the value is the number of members  
  
  
Example (using the Discord API guild):  
GET `https://discord.com/api/v8/guilds/81384788765712384/roles/member-counts`  
```
{
  "585569508501094449": 14,
  "159592059873787904": 45,
  "254077236989132800": 7,
  "187053776920641536": 420,
  "233981945279807488": 33
  trimmed...
}
```

### User Affinities

Unknown. Presumably values indicating who the user communicates with most  

#### Get User Affinities

GET `https://discord.com/api/v8/users/@me/affinities/users`  

Returns:

| Field           | Type                                                    | Description             |
|-----------------|---------------------------------------------------------|-------------------------|
| user_affinities | array of [user affinity](#user-affinity-object) objects | list of user affinities |
|

#### User Affinity Object

| Field    | Type           | Description              |
|----------|----------------|--------------------------|
| user_id  | snowflake      | the id of the user       |
| affinity | decimal number | the affinity of the user |
|

### Guild Affinities

Unknown. Presumably values indicating what guilds the user communicates in the most  

#### Get Guild Affinities

GET `https://discord.com/api/v8/users/@me/affinities/guilds`  

Returns:

| Field            | Type                                                      | Description              |
|------------------|-----------------------------------------------------------|--------------------------|
| guild_affinities | array of [guild affinity](#guild-affinity-object) objects | list of guild affinities |
|

#### Guild Affinity Object

| Field    | Type           | Description              |
|----------|----------------|--------------------------|
| guild_id | snowflake      | the id of the guild       |
| affinity | decimal number | the affinity of the guild |
|

### User Notes

#### Get User Note

GET `/users/@me/notes/{user.id}`

Returns a [user note object](#user-note-object) or a 404 if no note is set

#### Set User Note

PUT `/users/@me/notes/{user.id}`  
JSON parameters:

| Field | Type   | Description                    |
|-------|--------|--------------------------------|
| note  | string | the note to assign to the user |

Returns the new [user note object](#user-note-object)

#### User Note Update dispatch event

Sent whenever a user's note is updated

| Field | Type      | Description                                    |
|-------|-----------|------------------------------------------------|
| note  | string    | the note assigned to the user                  |
| id    | snowflake | the id of the user whose note has been updated |

#### User Note Object

Whether the fields are optional or can be null is unknown. In testing, they are always present and non-null

| Field | Type | Description |
|-------|------|-------------|
| note         | string    | the note assigned to the user                                           |
| note_user_id | snowflake | the id of the user with the note                                        |
| user_id      | snowflake | the id of the user who created the note (apparently always your own id) |
|


### User Profiles

#### Get User Profile

GET `/users/{user.id}/profile`  
Returns a [user profile object](#user-profile-object) or 404 if the user does not exist  
Note: a deleted guild can be returned in `mutual_guilds` (including the `nick` field), so do not assume all the guilds in `mutual_guilds` actually exist. The official client simply hides this information

#### User Profile Object

| Field                | Type                                                                          | Description
|----------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| user                 | [user object](https://discord.com/developers/docs/resources/user#user-object) | the user whose profile was requested                                     |
| ?premium_since       | ?string                                                                       | timestamp of when the user first purchased nitro(?)                      |
| ?premium_guild_since | ?string                                                                       | timestamp of when the user began boosting the guild                      |
| connected_accounts   | array of [connection objects](#connection-object)                             | list of the user's connected accounts                                    |
| mutual_guilds        | array of [mutual guild objects](#mutual-guild-object)                         | list of mutual guilds between the requesting user and the requested user |
|

#### Mutual Guild Object

| Field | Type      | Description                                |
|-------|-----------|--------------------------------------------|
| id    | snowflake | id of the guild                            |
| ?nick | string(?) | the requested user's nickname in the guild |
|

#### Connection Object

| Field    | Type   | Description                                                    |
|----------|--------|----------------------------------------------------------------|
| id       | string | unique identifier for the user's connection on the service     |
| type     | string | [type](#connection-types) of service the connection represents |
| name     | string | name of the user's connection. not necessarily unique          |
| verified | bool   | if the user's connection has been verified                     |
|

#### Connection Types
There may be more but this should be all of them
* battlenet
* facebook
* github
* reddit
* skype
* spotify
* steam
* twitch
* twitter
* xbox
* youtube
