### Modify Guild Extra Parameters

[Original documentation](https://discord.com/developers/docs/resources/guild#modify-guild)

Extra JSON parameters:

| Field    | Type              | Description |
|----------|-------------------|-------------|
| features | array of features | see below   |

The following features have been seen in Modify Guild:
* NEWS (sent along with DISCOVERABLE)
* COMMUNITY (sent when enabling community mode)
* DISCOVERABLE (sent when enabling guild discovery)

Additionally, setting `system_channel_id`, `rules_channel_id`, or `public_updates_channel_id`, to 1 in this endpoint (at least when adding the "COMMUNITY" feature) will create new channels
