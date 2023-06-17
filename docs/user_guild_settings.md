# User Guild Settings

Per-guild user settings

## User Guild Settings object

| Field   | Type                                                                            | Description                         |
|---------|---------------------------------------------------------------------------------|-------------------------------------|
| entries | array of [user guild settings entry objects](#user-guild-settings-entry-object) | entries for each guild              |
| partial | bool                                                                            |                                     |
| version | integer                                                                         | seems to increment for every update |


### User Guild Settings Entry Object

| Field                 | Type                                                          | Description                                                         |
|-----------------------|---------------------------------------------------------------|---------------------------------------------------------------------|
| channel_overrides     | array of [channel override objects](#channel-override-object) | overrides for specific channels                                     | 
| flags                 | [onboarding guild flags](#onboarding-guild-flags)             | used for community onboarding                                       |
| guild_id              | ?snowflake                                                    | the id of the guild this entry is for, or null for private channels |
| hide_muted_channels   | bool                                                          |                                                                     |
| message_notifications | [message notifications level](#message-notifications-level)   |                                                                     |
| mobile_push           | bool                                                          | send push notifications for this guild                              |
| mute_config           | [mute configuration object](#mute-configuration-object)       | used for mute for n minutes feature                                 |
| mute_scheduled_events | bool                                                          |                                                                     |
| muted                 | bool                                                          | is the guild currently muted                                        |
| notify_highlights     | bool                                                          |                                                                     |
| suppress_everyone     | bool                                                          | don't notify for @everyone                                          |
| suppress_roles        | bool                                                          | don't notify for @roles                                             |
| version               | integer                                                       | seems to increment for every update                                 |


### Channel Override Object

| Field                 | Type                                                        | Description                              |
|-----------------------|-------------------------------------------------------------|------------------------------------------|
| channel_id            | snowflake                                                   | the id for the channel this entry is for |
| collapsed             | bool                                                        |                                          |
| flags                 | [onboarding channel flags](#onboarding-channel-flags)       | used for community onboarding            |
| message_notifications | [message notifications level](#message-notifications-level) |                                          |
| mute_config           | [mute configuration object](#mute-configuration-object)     | used for mute for n minutes feature      |
| muted                 | bool                                                        | is the channel currently muted           |

### Mute Configuration Object

| Field                | Type                | Description                                      |
|----------------------|---------------------|--------------------------------------------------|
| end_time             | ?ISO-8601 timestamp | when the mute ends                               |
| selected_time_window | integer             | how many seconds the mute is for. -1 for forever |


### Message Notifications Level  <br>

| Key           | Value | Description                                                                                                     |
|---------------|-------|-----------------------------------------------------------------------------------------------------------------|
| ALL_MESSAGES  | 0     | receive notifications for all messages                                                                          |
| ONLY_MENTIONS | 1     | receive notifications only for messages that @mention the user                                                  |
| NO_MESSAGES   | 2     | don't receive notifications for any messages                                                                    |
| NULL          | 3     | use the parent's notification settings. e.g. a channel should use the notification level of its parent category |


#### Onboarding Guild Flags

| Key                             | Value | Description |
|---------------------------------|-------|-------------|
| UNREADS_ALL_MESSAGES            | 2048  |             |
| UNREADS_MENTIONS_AND_HIGHLIGHTS | 4096  |             |
| OPT_IN_CHANNELS_OFF             | 8192  |             |
| OPT_IN_CHANNELS_ON              | 16384 |             |


#### Onboarding Channel Flags

| Key                             | Value | Description |
|---------------------------------|-------|-------------|
| UNREADS_MENTIONS_AND_HIGHLIGHTS | 512   |             |
| UNREADS_ALL_MESSAGES            | 1024  |             |
| FAVORITED                       | 2048  |             |
| OPT_IN_ENABLED                  | 4096  |             |
| NEW_FORUM_THREADS_OFF           | 8192  |             |
| NEW_FORUM_THREADS_ON            | 16384 |             |

