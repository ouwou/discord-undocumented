* auto-gen TOC:
{:toc}

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
