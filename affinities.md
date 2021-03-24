### User Affinities

Unknown. Presumably values indicating who the user communicates with most  

#### Get User Affinities

GET `https://discord.com/api/v8/users/@me/affinities/users`  

Returns:

| Field           | Type                                                    | Description             |
|-----------------|---------------------------------------------------------|-------------------------|
| user_affinities | array of [user affinity](#user-affinity-object) objects | list of user affinities |

#### User Affinity Object

| Field    | Type           | Description              |
|----------|----------------|--------------------------|
| user_id  | snowflake      | the id of the user       |
| affinity | decimal number | the affinity of the user |

### Guild Affinities

Unknown. Presumably values indicating what guilds the user communicates in the most  

#### Get Guild Affinities

GET `https://discord.com/api/v8/users/@me/affinities/guilds`  

Returns:

| Field            | Type                                                      | Description              |
|------------------|-----------------------------------------------------------|--------------------------|
| guild_affinities | array of [guild affinity](#guild-affinity-object) objects | list of guild affinities |

#### Guild Affinity Object

| Field    | Type           | Description              |
|----------|----------------|--------------------------|
| guild_id | snowflake      | the id of the guild       |
| affinity | decimal number | the affinity of the guild |
