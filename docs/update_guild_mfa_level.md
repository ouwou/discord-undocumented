# Update Guild MFA Level

**POST** `/guilds/{guild.id}/mfa`<br>
Modify the MFA level of a guild. Can only be performed by the guild's owner

JSON parameters:

| Field | Type    | Description                               |
|-------|---------|-------------------------------------------|
| level | integer | 0 to disable MFA requirement, 1 to enable |
