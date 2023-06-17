# Bulk Add Member Role

**PATCH** `/guilds/{guild.id}/roles/{role.id}/members`<br>
Assign multiple members a role at once<br>
Returns map from user ids to [member objects](https://discord.com/developers/docs/resources/guild#guild-member-object)<br>

JSON parameters:

| Field      | Type               | Description                         |
|------------|--------------------|-------------------------------------|
| member_ids | array of snowflake | list of members to give the role to |
