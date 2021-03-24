### Ready Dispatch Event Extra Fields

| Field                | Type                                                                                 | Description                                                           |
| ---------------------|--------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| guild_join_requests? | array of [guild application objects](./member_verification#guild-application-object) | applications the user has made for guilds. used in verification gates |
| required_action?     | string                                                                               | see [required action type](#required-action-type)                     |
