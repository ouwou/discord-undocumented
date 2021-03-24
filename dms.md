### DMs

#### Create DM

POST `/users/@me/channels`  
Creates a new DM. Even though the official docs suggest a different request for creating a new DM with one user, the official client still uses a 1-element array.  
Returns a [channel object](https://discord.com/developers/docs/resources/channel#channel-object)

JSON parameters:

| Field      | Type               | Description                                     |
|------------|--------------------|-------------------------------------------------|
| recipients | array of snowflake | array of user ids who should be added to the dm |

#### Close DM

DELETE `/channels/{channel.id}`

#### Add Group DM Recipient

PUT `/channels/{channel.id}/recipients/{user.id}`

#### Remove Group DM Recipient

DELETE `/channels/{channel.id}/recipients/{user.id}`
