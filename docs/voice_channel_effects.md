### Voice Channel Effects

Voice channel effects are emojis that you can spam all over people's screens when they're tabbed into voice chat because that's a great feature I guess.

#### Voice Channel Effect Send Dispatch Event

| Field      | Type                                                                | Description                    |
|------------|---------------------------------------------------------------------|--------------------------------|
| user_id    | snowflake                                                           | user who sent the effect       |
| emoji      | [emoji object](https://discord.com/developers/docs/resources/emoji) | the sent emoji                 |
| channel_id | snowflake                                                           | channel the effect was sent to |
| guild_id   | snowflake                                                           | guild the channel belongs to   |


#### Send Voice Channel Effect

POST `/channels/{channel.id}/voice-channel-effects`<br>
Returns 204 No Content on success

JSON parameters:

| Field      | Type      | Description                                  |
|------------|-----------|----------------------------------------------|
| emoji_name | string    | name of the emoji or actual emoji if Unicode |
| emoji_id   | snowflake | id of the emoji or null if Unicode           |
