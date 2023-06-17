# Ready Event Extra Fields

| Field                | Type                                                                                  | Description                                                           |
| ---------------------|---------------------------------------------------------------------------------------|-----------------------------------------------------------------------|
| guild_join_requests? | array of [guild application objects](member_verification.md#guild-application-object) | applications the user has made for guilds. used in verification gates |
| required_action?     | string                                                                                | see [required action type](#required-action-type)                     |

## Required Action Type

| Type                   | Description                           |
|------------------------|---------------------------------------|
| AGREEMENTS             | user must accept new terms of service |
| REQUIRE_VERIFIED_EMAIL | user must verify their email          |
| REQUIRE_VERIFIED_PHONE | user must verify their phone          |
| REQUIRE_CAPTCHA        | user must complete a captcha          |
