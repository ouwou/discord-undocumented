# Affinities

As of June 2023, these endpoints appear to return the below objects, but with no data.

## User Affinities

Unknown. Presumably values indicating who the user communicates with most<br>

### Get User Affinities

**GET** `/users/@me/affinities/users`<br>

Returns:

| Field                   | Type                                                    | Description             |
|-------------------------|---------------------------------------------------------|-------------------------|
| user_affinities         | array of [user affinity](#user-affinity-object) objects | list of user affinities |
| inverse_user_affinities | unknown                                                 | unknown                 |

### User Affinity Object

| Field    | Type           | Description              |
|----------|----------------|--------------------------|
| user_id  | snowflake      | the id of the user       |
| affinity | decimal number | the affinity of the user |

## Guild Affinities

Unknown. Presumably values indicating what guilds the user communicates in the most<br>

### Get Guild Affinities

**GET** `/users/@me/affinities/guilds`<br>

Returns:

| Field            | Type                                                      | Description              |
|------------------|-----------------------------------------------------------|--------------------------|
| guild_affinities | array of [guild affinity](#guild-affinity-object) objects | list of guild affinities |

### Guild Affinity Object

| Field    | Type           | Description               |
|----------|----------------|---------------------------|
| guild_id | snowflake      | the id of the guild       |
| affinity | decimal number | the affinity of the guild |
