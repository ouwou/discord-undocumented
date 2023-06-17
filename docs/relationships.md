# User Relationships

## Get User Relationships

**GET** `/users/@me/relationships`<br>

Returns an array of [relationship objects](#relationship-object) with an extra key `type` representating the [relationship type](#relationship-type)

## Send Friend Request by Tag

**POST** `/users/@me/relationships`<br>

Returns a 204 on success<br>

JSON parameters:

| Field         | Type   | Description       |
|---------------|--------|-------------------|
| username      | string | the username      |
| discriminator | int    | the discriminator |

## Send Friend Request by ID or Accept Friend Request

**PUT** `/users/@me/relationships/{user.id}`<br>
Returns a 204 on success<br>

Request body must be `{}`

## Remove Relationship

**DELETE** `/users/@me/relationships/{user.id}`<br>
This is used for removing a friend or block, canceling an outgoing request, or ignoring an incoming request<br>

Returns a 204 on success

## Block User

**PUT** `/users/@me/relationships/{user.id}`<br>

Returns a 204 on success<br>

Request body must be `{"type":2}`

## Get Mutual Friends

**GET** `/users/{user.id}/relationships`<br>
Returns an array of [user objects](https://discord.com/developers/docs/resources/user#user-object)

## Modify Friend Nickname<br>

**GET** `/users/@me/relationships/{user.id}`<br>
Modifies the nickname of the friend<br>
Fires a RELATIONSHIP_UPDATE event containing a [relationship object](#relationship-object)

Returns 204 No Content on success

JSON parameters:

| Field    | Type    | Description             |
|----------|---------|-------------------------|
| nickname | string? | nickname for the friend |


## Relationship Type

| Type             | Value |
|------------------|-------|
| None             | 0     |
| Friend           | 1     |
| Blocked          | 2     |
| Pending Incoming | 3     |
| Pending Outgoing | 4     |
| Implicit         | 5     |

## Relationship Object

| Field    | Type                                                                          | Description                                    |
|----------|-------------------------------------------------------------------------------|------------------------------------------------|
| id       | snowflake                                                                     | id of the user who the relationship is between |
| type     | [relationship type](#relationship-type)                                       | type of the relationship                       |
| nickname | string?                                                                       | the friend's nickname                          |
| user?    | [user object](https://discord.com/developers/docs/resources/user#user-object) | the user                                       |

[Relationship objects](#relationship-object) can be found in the gateway READY event under the field `relationships`
