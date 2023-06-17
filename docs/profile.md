# User Profiles

## Get User Profile

**GET** `/users/{user.id}/profile`<br>
Returns a [user profile object](#user-profile-object) or 404 if the user does not exist<br>
Note: a deleted guild can be returned in `mutual_guilds` (including the `nick` field), so do not assume all the guilds in `mutual_guilds` actually exist. The official client simply hides this information

### User Profile Object

| Field                | Type                                                                          | Description                                                              |
|----------------------|-------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| user                 | [user object](https://discord.com/developers/docs/resources/user#user-object) | the user whose profile was requested*                                    |
| ?premium_since       | string?                                                                       | timestamp of when the user first purchased nitro(?)                      |
| ?premium_guild_since | string?                                                                       | timestamp of when the user began boosting the guild                      |
| connected_accounts   | array of [connection objects](#connection-object)                             | list of the user's connected accounts                                    |
| mutual_guilds        | array of [mutual guild objects](#mutual-guild-object)                         | list of mutual guilds between the requesting user and the requested user |

\* this user object may have extra fields such as profile customization information (see: [Profile Customation](./profile_customization))

### Mutual Guild Object

| Field | Type      | Description                                |
|-------|-----------|--------------------------------------------|
| id    | snowflake | id of the guild                            |
| ?nick | string    | the requested user's nickname in the guild |

### Connection Object

| Field    | Type   | Description                                                    |
|----------|--------|----------------------------------------------------------------|
| id       | string | unique identifier for the user's connection on the service     |
| type     | string | [type](#connection-types) of service the connection represents |
| name     | string | name of the user's connection. not necessarily unique          |
| verified | bool   | if the user's connection has been verified                     |

### Connection Types
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
