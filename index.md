* auto-gen TOC:
{:toc}

If a "(?)" is at the end of a field or type name it means it might be optional or nullable but is not known for sure

### Create Guild Extra Parameters

[Original documentation](https://discord.com/developers/docs/resources/guild#create-guild)

Extra JSON parameters:

| Field               | Type   | Description                             |
|---------------------|--------|-----------------------------------------|
| guild_template_code | string | template to use when creating the guild |

#### Guild Template Codes

| Code         | Description     |
|--------------|-----------------|
| 2TffvPucqHkN | Blank           |
| hvtBQMfw6uSJ | Gaming          |
| hgM48av5Q69A | Friends         |
| FbwUwRp4j8Es | Study           |
| s4WNnBxTDPsY | Clubs           |
| 6exdzMgjZgah | Creators        | 
| 64UDvRNCC52Y | Local Community |
| Ctg7PUHcQmZu | School Club     |

### Modify Guild Extra Parameters

[Original documentation](https://discord.com/developers/docs/resources/guild#modify-guild)

Extra JSON parameters:

| Field    | Type              | Description |
|----------|-------------------|-------------|
| features | array of features | see below   |

The following features have been seen in Modify Guild:
* NEWS
* COMMUNITY
* DISCOVERABLE

Additionally, setting `system_channel_id`, `rules_channel_id`, or `public_updates_channel_id`, to 1 in this endpoint (at least when adding the "COMMUNITY" feature) will create new channels

### Get Role Member Counts

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
&nbsp;  

### Get Role Members

GET `/guilds/{guild.id}/roles/{role.id}/member-ids`  
Retrieves up to 100 member IDs who have the given role  
Returns array of snowflakes  
&nbsp;  

### Bulk Add Member Role

PATCH `/guilds/{guild.id}/roles/{role.id}/members`  
Assign multiple members a role at once  
Returns array of [member objects](https://discord.com/developers/docs/resources/guild#guild-member-object)  
JSON parameters:

| Field      | Type               | Description                         |
|------------|--------------------|-------------------------------------|
| member_ids | array of snowflake | list of members to give the role to |

### Update Guild MFA Level

POST `/guilds/{guild.id}/mfa`  
Modify the MFA level of a guild. Can only be performed by the guild's owner  
JSON parameters:

| Field | Type    | Description                               |
|-------|---------|-------------------------------------------|
| level | integer | 0 to disable MFA requirement, 1 to enable |

### Join Guild

POST `/invites/{invite.code}`

### Leave Guild

DELETE `/users/@me/guilds/{guild.id}`

### Member Verification Gate and Guild Applications

Guilds with the feature `MEMBER_VERIFICATION_GATE_ENABLED` require new members to verify themselves  
Some of the unknown information is probably easy to find, but I don't have access to a community server  
Guilds may also create forms that users submit in order to apply for access to a guild  

#### Get Member Verification Gate

GET `/guilds/{guild.id}/member-verification`  
The official client adds parameters `with_guild=true` and `invite_code=` but these don't seem to do anything  
Returns a [verfication gate info object](#verification-gate-info-object) or 204 No Content if there is no verification gate

#### Modify Member Verification Gate

PATCH `/guilds/{guild.id}/member-verification`  
Request body is a partial [verfication gate info object](#verification-gate-info-object)  
Returns a [verfication gate info object](#verification-gate-info-object)

#### Verification Gate Info Object

| Field        | Type                                                                     | Description                                                                                     |
|--------------|--------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| ?description | string                                                                   | description of the server                                                                       |
| ?form_fields | array of [verification field objects](#verification-field-object)        | list of fields                                                                                  |
| ?version     | timestamp                                                                | string timestamp representing when the verification info was last updated                       |
| ?enabled     | bool                                                                     | seems to be present only in [Modify Member Verification Gate](#modify-member-verification-gate) |

#### Verification Field Object

| Field      | Type            | Description                                                             |
|------------|-----------------|-------------------------------------------------------------------------|
| field_type | string          | type of field. see below                                                |
| label      | string          | label of the field                                                      |
| required   | bool            | whether it is required to check the checkbox in order to submit         |
| values     | array of string | list of parameters for the field. see below                             |

#### Verification Field Type

| Name            | Description                                         |
|-----------------|-----------------------------------------------------|
| TERMS           | "Server Rules" `values` is a list of a server rules |
| TEXT_INPUT      | "Short Answer" `values` is unknown                  |
| PARAGRAPH       | "Paragraph" `values` is unknown                     |
| MULTIPLE_CHOICE | "Multiple Choice" `values` is unknown               |
| VERIFICATION    | "Connections" `values` is unknown                   |
| FILE_UPLOAD     | Not present in code; only a translation string      |

#### Request to Join Guild

PUT `/guilds/{guild.id}/requests/@me`  
Request body is the [verification info object](#verification-gate-info-object) the user accepted  
Returns 201 Created and a [guild application object](#guild-application-object) on success  

#### Guild Application Object

| Field              | Type      | Description                                            |
|--------------------|-----------|--------------------------------------------------------|
| application_status | string    | may be "STARTED", "PENDING", "REJECTED", or "APPROVED" |
| created_at         | timestamp | string timestamp when the application was created      |
| guild_id           | snowflake | id of the guild being applied to                       |
| last_seen          | timestamp | unknown                                                |
| rejection_reason   | string?   | reason for rejection (if rejected)                     |
| user_id            | snowflake | id of the user who created the application             |

### Welcome Screen

#### Get Welcome Screen

GET `/guilds/{guild.id}/welcome-screen`

Returns a [welcome screen object](https://discord.com/developers/docs/resources/guild#welcome-screen-object-welcome-screen-structure) or 204 No Content if there is none set  

#### Modify Welcome Screen

PATCH `/guilds/{guild.id}/welcome-screen`  
Request body is a [welcome screen object](https://discord.com/developers/docs/resources/guild#welcome-screen-object-welcome-screen-structure)  
Returns a [welcome screen object](https://discord.com/developers/docs/resources/guild#welcome-screen-object-welcome-screen-structure) on succses  

### Guild Discovery Catalog

#### Get Discovery Categories

GET `/discovery/categories`  
Returns array of [discovery category objects](#discovery-category-object) (unlocalized objects)  
GET parameters:

| Name         | Type   | Description                                   |
|--------------|--------|-----------------------------------------------|
| locale       | string | locale to return. doesn't seem to do anything |
| primary_only | bool   | only return primary-level categories          |

#### Discovery Category Object

| Field       | Type                                              | Description                        |
|------------|----------------------------------------------------|------------------------------------|
| id         | integer                                            | unique id for the category         |
| is_primary | bool                                               | is the category a primary category |
| name       | string or [localized name](#localized-name-object) | name of the category               |

#### Localized Name Object

| Field         | Type                                                   | Description                            |
|---------------|--------------------------------------------------------|----------------------------------------|
| default       | string                                                 | fallback localization string (english) |
| localizations | array of object, key is language code, value is string | localized versions of the string       |

#### Get Discoverable Guilds

GET `/discoverable-guilds`  
Returns [discoverable guilds response object](#discoverable-guilds-response-object)  
GET parameters:

| Name   | Type        | Description                    |
|--------|-------------|--------------------------------|
| offset | integer     | offset into the list of guilds |
| limit  | integer     | limit of guilds to get         |
| categories | integer | category to limit response to  |

#### Discoverable Guilds Response Object

| Field   | Type                                                                                                                   | Description                     |
|--------|------------------------------------------------------------------------------------------------------------------------|---------------------------------|
| limit  | integer                                                                                                                | limit given in request          |
| offset | integer                                                                                                                | offset given in request         |
| total  | integer                                                                                                                | total number of matching guilds |
| guilds | array of [guild objects](https://discord.com/developers/docs/resources/guild#guild-object) with extra keys (see below) | list of discoverable guilds     |

guilds object extra fields:

| Field                  | Type                                                                        | Description                |
|------------------------|-----------------------------------------------------------------------------|----------------------------|
| keywords               | array of string                                                             | keywords of the guild      |
| primary_category_id(?) | integer                                                                     | id of the primary category |
| categories             | array of localized [discovery category objects](#discovery-category-object) | categories of the guild    |
| auto_removed(?)        | bool(?)                                                                     | unknown                    |

#### Join Discoverable Guild

PUT `/guilds/{guild.id}/members/@me`  
Returns a [guild object](https://discord.com/developers/docs/resources/guild#guild-object)  
The official client also adds the GET parameters `lurker=false` though it's unclear what difference this makes

#### Searching Discoverable Guilds

Discord uses [Algolia](https://algolia.com) with key `NKTZZ4AIZU` to search for guilds which is beyond the scope of this page  
GET `/discovery/valid-term?term={term}` will return `{"valid": true}` if a search term is valid

### Guild Lurking

Guilds with the feature `PREVIEW_ENABLED` can be "lurked" in/previewed before actually joining. This is basically the same as joining except you are granted no permissions and are not counted as a member

#### Start Lurking

PUT `/guilds/{guild.id}/members/@me?lurker=true&session_id={session.id}`  
Session ID is presumably the one found in the READY gateway message and you will be removed when this session expires  
Returns a [guild object](https://discord.com/developers/docs/resources/guild#guild-object)

#### Stop Lurking

Same as [Leave Guild](#leave-guild)

### Managing Guild Discovery and Partnership

#### Get Guild Discovery Requirements

GET `/guilds/{guild.id}/discovery-requirements`  
Returns a [guild requirements object](#guild-requirements-object)

#### Get Guild Partnership Requirements

GET `/partners/{guild.id}/requirements`  
Returns a [guild requirements object](#guild-requirements-object)

#### Guild Requirements Object

| Field                           | Type                                              | Description                                  |
|---------------------------------|---------------------------------------------------|----------------------------------------------|
| age                             | bool                                              | is the guild old enough                      |
| engagement_healthy              | bool                                              | do members visit and talk enough             |
| health_score                    | object, unknown structure                         | unknown                                      |
| health_score_pending            | bool                                              | is waiting on server activity metrics           |
| healthy                         | bool                                              | are server activity requirements met         |
| nsfw_properties                 | [nsfw properties object](#nsfw-properties-object) | channels with meanie words in them           |
| protected                       | bool                                              | is 2FA enabled for moderators                |
| retention_healthy               | bool                                              | is member retention sufficient               |
| safe_environment                | bool                                              | if false, guild was flagged by Trust & Safety |
| size                            | bool                                              | are there enough members in the guild        |
| sufficient                      | bool                                              | are all requirements met                     |
| sufficient_without_grace_period | bool                                              | unknown                                      |
| minimum_age                     | integer                                           | how many days old the guild must be          |
| minimum_size                    | integer                                           | how many members the guild must have         |
| valid_rules_channel             | bool                                              | does the guild have a rules channel          |

#### NSFW Properties Object

| Field    | Type               | Description                      |
|----------|--------------------|----------------------------------|
| channels | array of snowflake | channels with unacceptable names |

### Thread Channels

Drafted [here](https://github.com/discord/discord-api-docs/pull/2693)

Used for ephemeral conversations started from existing channels. Users can join and leave threads. Can also be manually archived and unarchived

#### Create Thread

POST `/channels/{channel.id}/messages/{message.id}/threads`  
Creates a new thread starting in a channel attached to the given message.  
Unknown return  
JSON parameters:

| Field                 | Type   | Description                                                  |
|-----------------------|--------|--------------------------------------------------------------|
| auto_archive_duration | int    | minutes until the thread should be archived after inactivity |
| name                  | string | name of the thread                                           |
| type                  | int    | thread channel type. see [channel types](#channel-types)     |

#### Join Thread

POST `/channels/{thread.id}/thread-members/@me`  

#### Add Member to Thread

POST `/channels/{thread.id}/thread-members/{user.id}`

#### Leave Thread

DELETE `/channels/{thread.id}/thread-members/@me`

#### Modify Thread

PATCH `/channels/{thread.id}`  
JSON parameters:

| Field     | Type | Description                                                               |
|-----------|------|---------------------------------------------------------------------------|
| ?archived | bool | should the thread be archived                                             |
| ?auto_archive_duration | integer | minutes of inactivity until the thread should be archived |

#### Modify Notification Settings

PATCH `/channels/{thread.id}/thread-members/@me/settings`  
JSON parameters:

| Field | Type                                        | Description        |
|-------|---------------------------------------------|--------------------|
| flags | [thread member flags](#thread-member-flags) | notification flags |

#### Thread Member Flags

| Flag             | Value  |
|------------------|--------|
| HAS_PARTICIPATED | 1 << 0 |
| ALL_MESSAGES     | 1 << 1 |
| ONLY_MENTIONS    | 1 << 2 |
| NO_MESSAGES      | 1 << 3 |

#### Channel Types

| Type           | Value |
|----------------|-------|
| PUBLIC_THREAD  | 11    |
| PRIVATE_THREAD | 12    |

#### Message Types

| Type                   | Value |
|------------------------|-------|
| THREAD_STARTER_MESSAGE | 21    |

#### Message Flags

| Flag       | Value  |
|------------|--------|
| HAS_THREAD | 1 << 5 |

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

| Type              | Value |
|-------------------|-------|
| GUILD_STAGE_VOICE | 13    |

<details>
	<summary>show images</summary>
	<img src="media/stage_channel_list.png">
	<img src="media/stage_channel_perms.png">
	<img src="media/manage_stage_moderators.png">
</details>

### User Affinities

Unknown. Presumably values indicating who the user communicates with most  

#### Get User Affinities

GET `https://discord.com/api/v8/users/@me/affinities/users`  

Returns:

| Field           | Type                                                    | Description             |
|-----------------|---------------------------------------------------------|-------------------------|
| user_affinities | array of [user affinity](#user-affinity-object) objects | list of user affinities |

#### User Affinity Object

| Field    | Type           | Description              |
|----------|----------------|--------------------------|
| user_id  | snowflake      | the id of the user       |
| affinity | decimal number | the affinity of the user |

### Guild Affinities

Unknown. Presumably values indicating what guilds the user communicates in the most  

#### Get Guild Affinities

GET `https://discord.com/api/v8/users/@me/affinities/guilds`  

Returns:

| Field            | Type                                                      | Description              |
|------------------|-----------------------------------------------------------|--------------------------|
| guild_affinities | array of [guild affinity](#guild-affinity-object) objects | list of guild affinities |

#### Guild Affinity Object

| Field    | Type           | Description              |
|----------|----------------|--------------------------|
| guild_id | snowflake      | the id of the guild       |
| affinity | decimal number | the affinity of the guild |

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

#### Mutual Guild Object

| Field | Type      | Description                                |
|-------|-----------|--------------------------------------------|
| id    | snowflake | id of the guild                            |
| ?nick | string(?) | the requested user's nickname in the guild |

#### Connection Object

| Field    | Type   | Description                                                    |
|----------|--------|----------------------------------------------------------------|
| id       | string | unique identifier for the user's connection on the service     |
| type     | string | [type](#connection-types) of service the connection represents |
| name     | string | name of the user's connection. not necessarily unique          |
| verified | bool   | if the user's connection has been verified                     |

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

### User Relationships

#### Get User Relationships

GET `/users/@me/relationships`  
Returns an array of [user objects](https://discord.com/developers/docs/resources/user#user-object) with an extra key `type` representating the [relationship type](#relationship-type)

#### Get Mutual Friends

GET `/users/{user.id}/relationships`  
Returns an array of [user objects](https://discord.com/developers/docs/resources/user#user-object)

#### Relationship Type

| Type             | Value |
|------------------|-------|
| None             | 0     |
| Friend           | 1     |
| Blocked          | 2     |
| Pending Incoming | 3     |
| Pending Outgoing | 4     |
| Implicit         | 5     |

#### Relationship Object

| Field | Type                                    | Description                                    |
|-------|-----------------------------------------|------------------------------------------------|
| id    | snowflake                               | id of the user who the relationship is between |
| type  | [relationship type](#relationship-type) | type of the relationship                       |

[Relationship objects](#relationship-object) can be found in the gateway READY event under the field `relationships`

### DMs

#### Create DM

POST `/users/@me/channels`  
Creates a new DM. Even though the official docs suggest a different request for creating a new DM with one user, the official client still uses a 1-element array.  
Returns a [channel object](https://discord.com/developers/docs/resources/channel#channel-object)

JSON parameters:

| Field      | Type               | Description                                     |
|------------|--------------------|-------------------------------------------------|
| recipients | array of snowflake | array of user ids who should be added to the dm |

#### Close DM

DELETE `/channels/{channel.id}`

#### Add Group DM Recipient

PUT `/channels/{channel.id}/recipients/{user.id}`

#### Remove Group DM Recipient

DELETE `/channels/{channel.id}/recipients/{user.id}`

### Ready Supplemental Dispatch Event

This event appears to change every once in a while so these docs might be out of date (probably not)  
The ordering of the `merged_members` field appears to match that of the `guilds` array sent in the READY event

| Field            | Type                                                                                                        | Description                                           |
|------------------|-------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| merged_presences | [merged presences object](#merged-presences-object)                                                         | presences of friends and various users in guilds      |
| merged_members   | array of array of [member objects](https://discord.com/developers/docs/resources/guild#guild-member-object) | various members in guilds                             |
| guilds           | array                                                                                                       | appears to contain information regarding voice states |

#### Merged Presences Object

Similar the READY_SUPPLEMENTAL's `guild_members` field, the `guilds` array's ordering appears to match that of the `guilds` array sent in the READY event

| Field   | Type                                                                                                                                                                                     | Description                       |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|
| guilds  | array of objects similar to [presence](#https://discord.com/developers/docs/topics/gateway#presence-update-presence-update-event-fields) except `user_id` is always present and not `id` | the presence of a user in a guild |
| friends | same as above                                                                                                                                                                            | the presence of a friend          |
