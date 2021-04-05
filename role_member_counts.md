### Get Role Member Counts

Retrieves the number of members with each role  
[GitHub issue](https://github.com/discord/discord-api-docs/issues/2610#issuecomment-778985709)

GET `/api/guilds/{guild.id}/roles/member-counts`  
Returns json object where the key is the role ID and the value is the number of members  
Appears to require VIEW_AUDIT_LOG permission  
  
  
Example (using the Discord API guild):  
GET `https://discord.com/api/v8/guilds/81384788765712384/roles/member-counts`  
```
{
  "585569508501094449": 14,
  "159592059873787904": 45,
  "254077236989132800": 7,
  "187053776920641536": 420,
  "233981945279807488": 33
  trimmed...
}
```
