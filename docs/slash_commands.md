# Slash Commands

## Query Application Commands

Opcode 24 is used to request the application commands in a guild. The gateway will respond with a `GUILD_APPLICATION_COMMANDS_UPDATE`<br>
JSON parameters:

| Field           | Type      | Description                                                                  |
|-----------------|-----------|------------------------------------------------------------------------------|
| guild_id        | snowflake | guild to request application commands for                                    |
| applications    | bool      | should the applications field be sent                                        |
| nonce           | string    | unique value to differentiate responses. discord uses an incrementing number |
| offset          | int       | offset into list of commands                                                 |
| limit           | int       | max commands (discord uses 10)                                               |
| application_id? | ?         | ?                                                                            |

## GUILD_APPLICATION_COMMANDS_UPDATE

| Field                | Type                                                                                                                                                                                 | Description                                    |
|----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------|
| nonce                | string                                                                                                                                                                               | nonce sent in the request                      |
| updated_at           | unix timestamp                                                                                                                                                                       | ?                                              |
| guild_id             | snowflake                                                                                                                                                                            | guild the response is for                      |
| applications         | array of [application objects](#application-object)                                                                                                                                  | all applications for which there are commands  |
| application_commands | array of [ApplicationCommand](https://discord.com/developers/docs/interactions/slash-commands#applicationcommand) with [additional undocumented fields](#application-command-object) | the application commands                       |

### Application Object

| Field         | Type      | Description                                                     |
|---------------|-----------|-----------------------------------------------------------------|
| bot           | user      | the bot managing the commands                                   |
| command_count | int       | number of commands                                              |
| icon          | string    | icon hash                                                       |
| id            | snowflake | id of the application. can be equal to the bot's id             |
| name          | string    | name of the application. usually the same as the bot's username |

## Application Command Object
Undocumented fields for [ApplicationCommand](#https://discord.com/developers/docs/interactions/slash-commands#application-command-object)

| Field      | Type                                                                                                                                                | Description                 |
|------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------|
| version    | snowflake                                                                                                                                           | unknown                     |
| permission | array of [ApplicationCommandPermissions](#https://discord.com/developers/docs/interactions/slash-commands#application-command-permissions-object-application-command-permissions-structure) (probably) | permissions for the command |

