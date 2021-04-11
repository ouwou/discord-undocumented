### User Relationships

#### Get User Relationships

GET `/users/@me/relationships`  
Returns an array of [user objects](https://discord.com/developers/docs/resources/user#user-object) with an extra key `type` representating the [relationship type](#relationship-type)

#### Get Mutual Friends

GET `/users/{user.id}/relationships`  
Returns an array of [user objects](https://discord.com/developers/docs/resources/user#user-object)

### Modify Friend Nickname  

GET `/users/@me/relationships/{user.id}`  
Modifies the nickname of the friend  
Returns 204 No Content on success  
Fires a RELATIONSHIP_UPDATE event containing a [relationship object](#relationship-object)  
JSON parameters:  

| Field    | Type    | Description             |
|----------|---------|-------------------------|
| nickname | string? | nickname for the friend |


#### Relationship Type

| Type             | Value |
|------------------|-------|
| None             | 0     |
| Friend           | 1     |
| Blocked          | 2     |
| Pending Incoming | 3     |
| Pending Outgoing | 4     |
| Implicit         | 5     |

#### Relationship Object

| Field    | Type                                    | Description                                    |
|----------|-----------------------------------------|------------------------------------------------|
| id       | snowflake                               | id of the user who the relationship is between |
| type     | [relationship type](#relationship-type) | type of the relationship                       |
| nickname | string?                                 | the friend's nickname                          |

[Relationship objects](#relationship-object) can be found in the gateway READY event under the field `relationships`
