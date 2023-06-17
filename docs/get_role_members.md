# Get Role Members

**GET** `/guilds/{guild.id}/roles/{role.id}/member-ids`<br>
Retrieves up to 100 member IDs who have the given role<br>
Appears to require VIEW_AUDIT_LOG permission<br>

Returns array of snowflakes
