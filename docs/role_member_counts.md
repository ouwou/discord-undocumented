# Get Role Member Counts

Retrieves the number of members with each role (roughly.)<br>

**GET** `/api/guilds/{guild.id}/roles/member-counts`<br>
Appears to require VIEW_AUDIT_LOG permission

Returns JSON object where the key is the role ID and the value is the number of members<br>
<br>
???+ example
     Example (using the Discord API guild):<br>
     GET `https://discord.com/api/v9/guilds/81384788765712384/roles/member-counts`<br>
     ```json
     {
       "585569508501094449": 14,
       "159592059873787904": 45,
       "254077236989132800": 7,
       "187053776920641536": 420,
       "233981945279807488": 33
       trimmed...
     }
     ```
