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
