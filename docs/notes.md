# User Notes

## Get User Note

**GET** `/users/@me/notes/{user.id}`

Returns a [user note object](#user-note-object) or a 404 if no note is set

## Set User Note

**PUT** `/users/@me/notes/{user.id}`<br>
JSON parameters:

| Field | Type   | Description                    |
|-------|--------|--------------------------------|
| note  | string | the note to assign to the user |

Returns the new [user note object](#user-note-object)

### User Note Update dispatch event

Sent whenever a user's note is updated

| Field | Type      | Description                                    |
|-------|-----------|------------------------------------------------|
| note  | string    | the note assigned to the user                  |
| id    | snowflake | the id of the user whose note has been updated |

### User Note Object

Whether the fields are optional or can be null is unknown. In testing, they are always present and non-null

| Field        | Type      | Description                                                             |
|--------------|-----------|-------------------------------------------------------------------------|
| note         | string    | the note assigned to the user                                           |
| note_user_id | snowflake | the id of the user with the note                                        |
| user_id      | snowflake | the id of the user who created the note (apparently always your own id) |
