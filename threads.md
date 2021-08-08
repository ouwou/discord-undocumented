### Thread Channels

Threads are officially documented but there are some differences between the documentation designed for bot developers and what the client actually does

#### Thread Objects (extra fields)

| Field              | Type               | Description                                        |
|--------------------|--------------------|----------------------------------------------------|
| member_ids_preview | array of snowflake | contains a few ids of members for preview purposes |

#### Thread List Sync (extra fields)

Thread List Sync appears to always be sent when opening a channel as part of the lazy load request. It also seems to always send the status of the entire guild and never just specific channels

| Field                   | Type                     | Description                                  |
|-------------------------|--------------------------|----------------------------------------------|
| most_recent_messages(?) | array of message objects | contains a few messages for preview purposes |