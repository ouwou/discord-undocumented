# Gateway Opcodes

| Opcode | Name                                     | Documented | Client Action | Description                                                                             |
|--------|------------------------------------------|------------|---------------|-----------------------------------------------------------------------------------------|
| 0      | DISPATCH                                 | ✅          | Receive       | An event was dispatched.                                                                |
| 1      | HEARTBEAT                                | ✅          | Send/Receive  | Fired periodically by the client to keep the connection alive.                          |
| 2      | IDENTIFY                                 | ✅          | Send          | Starts a new session during the initial handshake.                                      |
| 3      | PRESENCE_UPDATE                          | ✅          | Send          | Update the client's presence.                                                           |
| 4      | VOICE_STATE_UPDATE                       | ✅          | Send          | Used to join/leave or move between voice channels.                                      |
| 5      | VOICE_SERVER_PING                        | ❌          | Send          |                                                                                         |
| 6      | RESUME                                   | ✅          | Send          | Resume a previous session that was disconnected.                                        |
| 7      | RECONNECT                                | ✅          | Receive       | You should attempt to reconnect and resume immediately.                                 |
| 8      | REQUEST_GUILD_MEMBERS                    | ✅          | Send          | Request information about offline guild members in a large guild.                       |
| 9      | INVALID_SESSION                          | ✅          | Receive       | The session has been invalidated. You should reconnect and identify/resume accordingly. |
| 10     | HELLO                                    | ✅          | Receive       | Sent immediately after connecting, contains the `heartbeat_interval` to use.            |
| 11     | HEARTBEAT_ACK                            | ✅          | Receive       | Sent in response to receiving a heartbeat to acknowledge that it has been received.     |
| 13     | CALL_CONNECT                             | ❌          | Send          |                                                                                         |
| 14     | GUILD_SUBSCRIPTIONS                      | ❌          | Send          | Subscribe to sections of a guild's member list.                                         |
| 15     | LOBBY_CONNECT                            | ❌          | Send          | Related to game invites/rich presence                                                   |
| 16     | LOBBY_DISCONNECT                         | ❌          | Send          | Related to game invites/rich presence                                                   |
| 17     | LOBBY_VOICE_STATES_UPDATE                | ❌          | Send          | Related to game invites/rich presence                                                   |
| 18     | STREAM_CREATE                            | ❌          | Send          | Start a stream.                                                                         |
| 19     | STREAM_DELETE                            | ❌          | Send          | End a stream or stop watching one.                                                      |
| 20     | STREAM_WATCH                             | ❌          | Send          | Joining a stream.                                                                       |
| 21     | STREAM_PING                              | ❌          | Send          |                                                                                         |
| 22     | STREAM_SET_PAUSED                        | ❌          | Send          | Mark a stream as paused or unpaused.                                                    |
| 24     | REQUEST_GUILD_APPLICATION_COMMANDS       | ❌          | Send          | Potentially unused.                                                                     |
| 25     | EMBEDDED_ACTIVITY_LAUNCH                 | ❌          | Send          | Potentially unused.                                                                     |
| 26     | EMBEDDED_ACTIVITY_CLOSE                  | ❌          | Send          | Leave an activity in a voice channel.                                                   |
| 27     | EMBEDDED_ACTIVITY_UPDATE                 | ❌          | Send          | Potentially unused.                                                                     |
| 28     | REQUEST_FORUM_UNREADS                    | ❌          | Send          | Request the unread state of a forum channel.                                            |
| 29     | REMOTE_COMMAND                           | ❌          | Send          |                                                                                         |
| 30     | GET_DELETED_ENTITY_IDS_NOT_MATCHING_HASH | ❌          | Send          |                                                                                         |
| 31     | REQUEST_SOUNDBOARD_SOUNDS                | ❌          | Send          | Request guilds' soundboards                                                             |
| 32     | SPEED_TEST_CREATE                        | ❌          | Send          |                                                                                         |
| 33     | SPEED_TEST_DELETE                        | ❌          | Send          |                                                                                         |
| 34     | REQUEST_LAST_MESSAGES                    | ❌          | Send          | Potentially unused.                                                                     |
| 35     | SEARCH_RECENT_MEMBERS                    | ❌          | Send          | Potentially unused.                                                                     |

## VOICE_SERVER_PING

Unknown. `d` is null

## CALL_CONNECT

Unknown.

| Field      | Type | Description |
|------------|------|-------------|
| channel_id |      |             |

## LOBBY_CONNECT

| Field        | Type | Description |
|--------------|------|-------------|
| lobby_id     |      |             |
| lobby_secret |      |             |

## LOBBY_DISCONNECT

| Field    | Type | Description |
|----------|------|-------------|
| lobby_id |      |             |

## LOBBY_VOICE_STATES_UPDATE

| Field     | Type | Description |
|-----------|------|-------------|
 | lobby_id  |      |             |
| self_mute |      |             |
| self_deaf |      |             |

## STREAM_CREATE

Used to start a stream.

| Field            | Type      | Description                              |
|------------------|-----------|------------------------------------------|
| type             | string    | type of the stream. `guild`              |
| guild_id         | snowflake | guild the stream is in                   |
| channel_id       | snowflake | channel the stream is in                 |
| preferred_region | string    | preferred region to create the stream in |

## STREAM_DELETE

Used to leave/end a stream

| Field      | Type   | Description                 |
|------------|--------|-----------------------------|
| stream_key | string |                             |

## STREAM_WATCH

Used when joining a stream.

| Field      | Type   | Description    |
|------------|--------|----------------|
| stream_key | string | stream to join |

## STREAM_PING

Unknown. `d` contains key `stream_key`

## STREAM_SET_PAUSED

Used to mark a stream as paused or unpaused

| Field      | Type    | Description                              |
|------------|---------|------------------------------------------|
| stream_key | string  | stream key to mark as paused or unpaused |
| paused     | boolean | is the stream paused                     |

## EMBEDDED_ACTIVITY_CLOSE

Used when leaving an activity in a voice channel.

| Field          | Type       | Description                   |
|----------------|------------|-------------------------------|
| guild_id       | ?snowflake | guild id the activity is in   |
| channel_id     | snowflake  | channel id the activity is in |
| application_id | snowflake  |                               |

## REQUEST_FORUM_UNREADS

Used to request the unread state of a forum channel. Gateway will send a `FORUM_UNREADS` dispatch event in response.

| Field      | Type             | Description                               |
|------------|------------------|-------------------------------------------|
| guild_id   | snowflake        | guild id of the forum channel             |
| channel_id | snowflake        | channel id of the forum channel           |
| threads    | thread subobject | list of threads to fetch unread state for |

### Thread subobject

| Field          | Type      | Description             |
|----------------|-----------|-------------------------|
| thread_id      | snowflake | thread id               |
| ack_message_id | snowflake | id of last read message |

## GET_DELETED_ENTITY_IDS_NOT_MATCHING_HASH

| Field            | Type            | Description |
|------------------|-----------------|-------------|
| guild_id         | snowflake       |             |
| channel_ids_hash | array of string |             |
 | role_ids_hash    | array of string |             |
| emoji_ids_hash   | array of string |             |
| sticker_ids_hash | array of string |             |

## REQUEST_SOUNDBOARD_SOUNDS

Request guilds' soundboards. Gateway will fire a `SOUNDBOARD_SOUNDS` dispatch event for each requested guild.

| Field     | Type               | Description                     |
|-----------|--------------------|---------------------------------|
| guild_ids | array of snowflake | guilds to fetch soundboards for |

## SPEED_TEST_CREATE

Unknown.

| Field            | Type | Description |
|------------------|------|-------------|
| preferred_region |      |             |

## SPEED_TEST_DELETE

Unknown. `d` is null.

## REQUEST_LAST_MESSAGES

Unknown.

| Field       | Type | Description |
|-------------|------|-------------|
| guild_id    |      |             |
| channel_ids |      |             |

## SEARCH_RECENT_MEMBERS

Unknown.

| Field              | Type | Description |
|--------------------|------|-------------|
| guild_id           |      |             |
| query              |      |             |
| continuation_token |      |             |
