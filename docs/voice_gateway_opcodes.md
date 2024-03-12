# Voice Gateway Opcodes

| Opcode | Name                                      | Documented | Client Action | Description                                                                                                  |
|--------|-------------------------------------------|------------|---------------|--------------------------------------------------------------------------------------------------------------|
| 0      | IDENTIFY                                  | ✅          | Send          | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 1      | SELECT_PROTOCOL                           | ✅          | Send          | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 2      | READY                                     | ✅          | Receive       | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 3      | HEARTBEAT                                 | ✅          | Send          | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 4      | SELECT_PROTOCOL_ACK                       | ✅          | Receive       | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 5      | SPEAKING                                  | ✅          | Send/Receive  | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 6      | HEARTBEAT_ACK                             | ✅          | Receive       | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 7      | RESUME                                    | ✅          | Send          | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 8      | HELLO                                     | ✅          | Receive       | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 9      | RESUMED                                   | ✅          | Receive       | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 12     | VIDEO                                     | ❌          |               | Used for when users enable their camera                                                                      |
| 13     | CLIENT_DISCONNECT                         | ✅          | Receive       | See [official docs](https://discord.com/developers/docs/topics/opcodes-and-status-codes#voice-voice-opcodes) |
| 14     | SESSION_UPDATE                            | ❌          |               |                                                                                                              |
| 15     | MEDIA_SINK_WANTS                          | ❌          | Receive       |                                                                                                              |
| 16     | VOICE_BACKEND_VERSION                     | ❌          | Send/Receive  |                                                                                                              |
| 17     | CHANNEL_OPTIONS_UPDATE                    | ❌          | Receive       |                                                                                                              |
| 18     | [FLAGS](#flags)                           | ❌          | Receive       | Per-user voice flags                                                                                         |
| 19     | SPEED_TEST                                | ❌          | Receive       |                                                                                                              |
| 20     | [PLATFORM](#platform)                     | ❌          | Receive       | Per-user platform information                                                                                |
| 21     | SECURE_FRAMES_PREPARE_PROTOCOL_TRANSITION | ❌          | Receive       |                                                                                                              |
| 22     | SECURE_FRAMES_EXECUTE_TRANSITION          | ❌          | Receive       |                                                                                                              |
| 23     | SECURE_FRAMES_READY_FOR_TRANSITION        | ❌          |               |                                                                                                              |
| 24     | SECURE_FRAMES_PREPARE_EPOCH               | ❌          | Receive       |                                                                                                              |
| 25     | MLS_EXTERNAL_SENDER_PACKAGE               | ❌          | Receive       |                                                                                                              |
| 26     | MLS_KEY_PACKAGE                           | ❌          |               |                                                                                                              |
| 27     | MLS_PROPOSALS                             | ❌          | Receive       |                                                                                                              |
| 28     | MLS_COMMIT_WELCOME                        | ❌          |               |                                                                                                              |
| 29     | MLS_PREPARE_COMMIT_TRANSITION             | ❌          | Receive       |                                                                                                              |
| 30     | MLS_WELCOME                               | ❌          | Receive       |                                                                                                              |

## FLAGS

| Field   | Type                        | Description             |
|---------|-----------------------------|-------------------------|
| user_id | snowflake                   | user the flags apply to |
| flags   | [voice flags](#voice-flags) | flags                   |

### Voice Flags

| Key    | Value                  | Description |
|--------|------------------------|-------------|
| 1 << 0 | CLIPS_ENABLED          |             |
| 1 << 1 | ALLOW_VOICE_RECORDING  |             |
| 1 << 2 | ALLOW_ANY_VIEWER_CLIPS |             |

## PLATFORM

description is a guess

| Field    | Type                            | Description              |
|----------|---------------------------------|--------------------------|
| user_id  | snowflake                       | user to set platform for |
| platform | [platform type](#platform-type) | their platform           |

### Platform Type

| Key | Value       |
|-----|-------------|
| 0   | DESKTOP     |
| 1   | MOBILE      |
| 2   | XBOX        |
| 3   | PLAYSTATION |
