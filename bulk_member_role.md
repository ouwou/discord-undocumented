### Bulk Add Member Role

PATCH `/guilds/{guild.id}/roles/{role.id}/members`  
Assign multiple members a role at once  
Returns array of [member objects](https://discord.com/developers/docs/resources/guild#guild-member-object)  
JSON parameters:

| Field      | Type               | Description                         |
|------------|--------------------|-------------------------------------|
| member_ids | array of snowflake | list of members to give the role to |
