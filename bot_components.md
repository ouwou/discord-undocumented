### (Undocumented) Bot Components

Bot components are now documented [here](https://discord.com/developers/docs/interactions/message-components)

Clicking a button causes a POST to Create Interaction with the `data` field being an object containing keys `component_type` (integer) and `custom_id` (string)

#### Component Type

| Name       | Value |
| select     | 3     |
