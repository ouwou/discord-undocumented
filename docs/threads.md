# Threads

Threads are officially documented but there are some differences between the documentation designed for bot developers and what the client actually does

## Member List

The client sends an Opcode 14 Lazy Request when a thread is opened:

| Field               | Type               | Description                                |
|---------------------|--------------------|--------------------------------------------|
| guild_id            | snowflake          | guild the thread is in                     |
| thread_member_lists | array of snowflake | threads to receive member list updates for |

## Thread Member List Update

This is sent to the client in response to the above request. THREAD_MEMBERS_UPDATE and THREAD_MEMBER_UPDATE are sent as documented to update the list

| Field     | Type                                                                                               | Description                             |
|-----------|----------------------------------------------------------------------------------------------------|-----------------------------------------|
| thread_id | snowflake                                                                                          | thread for which members are being sent |
| guild_id  | snowflake                                                                                          | guild the thread is in                  |
| members   | array of [member objects](https://discord.com/developers/docs/resources/guild#guild-member-object) | current members of the thread           |

## Thread Objects (extra fields)

| Field              | Type               | Description                                        |
|--------------------|--------------------|----------------------------------------------------|
| member_ids_preview | array of snowflake | contains a few ids of members for preview purposes |

## Thread List Sync (extra fields)

Thread List Sync appears to always be sent when opening a channel as part of the lazy load request. It also seems to always send the status of the entire guild and never just specific channels

| Field                   | Type                     | Description                                  |
|-------------------------|--------------------------|----------------------------------------------|
| most_recent_messages(?) | array of message objects | contains a few messages for preview purposes |