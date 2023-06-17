# Capabilities

Capabilities is a field (`capabilities`) within the IDENTIFY payload that communicates what the client is "capable" of.
Unfortunately this means Discord's API does weird things that don't match what the documentation says.

The following table is adapted from [here](https://github.com/MateriiApps/OpenCord/blob/ca334e382d1feecafcb99c3758a5b1133d130b13/app/src/main/java/com/xinto/opencord/gateway/io/Capabilities.kt)
since Discord hardcodes the `capabilities` value instead of using an enum so there are no official names.

| Key                                   | Value   | Description                                           |
|---------------------------------------|---------|-------------------------------------------------------|
| LAZY_USER_NOTES                       | 1 << 0  | don't send user notes in `READY`                      |
| NO_AFFINE_USER_IDS                    | 1 << 1  |                                                       |
| VERSIONED_READ_STATES                 | 1 << 2  |                                                       |
| VERSIONED_USER_GUILD_SETTINGS         | 1 << 3  |                                                       |
| DEDUPLICATE_USER_OBJECTS              | 1 << 4  |                                                       |
| PRIORITIZED_READY_PAYLOAD             | 1 << 5  | responsible for sending `READY_SUPPLEMENTAL           |
| MULTIPLE_GUILD_EXPERIMENT_POPULATIONS | 1 << 6  |                                                       |
| NON_CHANNEL_READ_STATES               | 1 << 7  |                                                       |
| AUTH_TOKEN_REFRESH                    | 1 << 8  |                                                       |
| USER_SETTINGS_PROTO                   | 1 << 9  | `user_settings` in the READY message will be omitted  |
| CLIENT_STATE_V2                       | 1 << 10 | heavily alters the guild object                       |
| PASSIVE_GUILD_UPDATE                  | 1 << 11 | causes the gateway to send `PASSIVE_UPDATE_V1` events |
| Unnamed bit 12                        | 1 << 12 | unknown                                               |

As of June 2023, Discord uses 8189 which corresponds to all bits except NO_AFFINE_USER_IDS

## USER_SETTINGS_PROTO

Forces usage of the `user_settings_proto` field which uses Google's protobuf instead of the standard `user_settings`.
The reconstructed .proto is available
[here](https://github.com/dolfies/discord-protos/blob/master/discord_protos/PreloadedUserSettings.proto)

## CLIENT_STATE_V2

The following fields of the [guild object](https://discord.com/developers/docs/resources/guild#guild-object-guild-structure)
are moved into a new field called `properties`:

* `afk_channel_id`
* `afk_timeout`
* `application_id`
* `banner`
* `default_message_notifications`
* `description`
* `discovery_splash`
* `explicit_content_filter`
* `features`
* `guild_hashes` (removed)
* `home_header`
* `hub_type`
* `icon`
* `latest_onboarding_question_id`
* `max_members`
* `max_stage_video_channel_users`
* `max_video_channel_users`
* `mfa_level`
* `name`
* `nsfw`
* `nsfw_level`
* `owner_id`
* `preferred_locale`
* `premium_progress_bar_enabled`
* `premium_tier`
* `public_updates_channel_id`
* `region` (removed)
* `rules_channel_id`
* `safety_alerts_channel_id`
* `splash`
* `system_channel_flags`
* `system_channel_id`
* `vanity_url_code`
* `verification_level`

The `version` field in channel and other objects within guild are removed.

The `data_mode` field is added to the guild object. Currently seems to always be "full."

## PASSIVE_GUILD_UPDATE

Causes a `PASSIVE_UPDATE_V1` dispatch event to be sent periodically instead of `CHANNEL_UNREADS_UPDATE`

### PASSIVE_UPDATE_V1 object

| Field        | Type                                                                                                                    | Description                         |
|--------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------------------|
| voice_states | array of [voice state](https://discord.com/developers/docs/resources/voice#voice-state-object-voice-state-structure)    | voice states for users in the guild |
| members      | array of [guild member](https://discord.com/developers/docs/resources/guild#guild-member-object-guild-member-structure) | some of the members                 |
| guild_id     | snowflake                                                                                                               | the guild the update is for         |
| channels     | array of read state entries                                                                                             | read state of the guild             |

## Unnamed bit 12

Behavior unknown. Only changed observed so far is `CALL_CREATE` events being fired for calls that are active at time of
connection
