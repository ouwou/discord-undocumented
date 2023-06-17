# Member Verification

## Member Verification Gate and Guild Applications

Guilds with the feature `MEMBER_VERIFICATION_GATE_ENABLED` require new members to verify themselves<br>
Guilds may also create forms that users submit in order to apply for access to a guild<br>

## Get Member Verification Gate

**GET** `/guilds/{guild.id}/member-verification`<br>
The official client adds parameters `with_guild=true` and `invite_code=` but these don't seem to do anything<br>
Returns a [verfication gate info object](#verification-gate-info-object) or 204 No Content if there is no verification gate

## Modify Member Verification Gate

**PATCH** `/guilds/{guild.id}/member-verification`<br>
Request body is a partial [verfication gate info object](#verification-gate-info-object)<br>
Returns a [verfication gate info object](#verification-gate-info-object)

### Verification Gate Info Object

| Field        | Type                                                                     | Description                                                                                     |
|--------------|--------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| description? | string                                                                   | description of the server                                                                       |
| form_fields? | array of [verification field objects](#verification-field-object)        | list of fields                                                                                  |
| version?     | timestamp                                                                | string timestamp representing when the verification info was last updated                       |
| enabled?     | bool                                                                     | seems to be present only in [Modify Member Verification Gate](#modify-member-verification-gate) |

### Verification Field Object

| Field      | Type            | Description                                                             |
|------------|-----------------|-------------------------------------------------------------------------|
| field_type | string          | type of field. see below                                                |
| label      | string          | label of the field                                                      |
| required   | bool            | whether it is required to check the checkbox in order to submit         |
| response   | bool            | true to indicate the terms were accepted                                |
| values     | array of string | list of parameters for the field. see below                             |

### Verification Field Type

| Name            | Description                                         |
|-----------------|-----------------------------------------------------|
| TERMS           | "Server Rules" `values` is a list of a server rules |
| TEXT_INPUT      | "Short Answer" `values` is unknown                  |
| PARAGRAPH       | "Paragraph" `values` is unknown                     |
| MULTIPLE_CHOICE | "Multiple Choice" `values` is unknown               |
| VERIFICATION    | "Connections" `values` is unknown                   |
| FILE_UPLOAD     | Not present in code; only a translation string      |

## Request to Join Guild

**PUT** `/guilds/{guild.id}/requests/@me`<br>
Request body is the [verification info object](#verification-gate-info-object) the user accepted<br>
Returns 201 Created and a [guild application object](#guild-application-object) on success<br>

### Guild Application Object

| Field              | Type                                                                          | Description                                            |
|--------------------|-------------------------------------------------------------------------------|--------------------------------------------------------|
| application_status | string                                                                        | may be "STARTED", "PENDING", "REJECTED", or "APPROVED" |
| created_at         | ?timestamp                                                                    | string timestamp when the application was created      |
| guild_id           | snowflake                                                                     | id of the guild being applied to                       |
| last_seen          | ?timestamp                                                                    | unknown                                                |
| rejection_reason   | ?string                                                                       | reason for rejection (if rejected)                     |
| user_id            | snowflake                                                                     | id of the user who created the application             |
| user?              | [user object](https://discord.com/developers/docs/resources/user#user-object) | the user who created the request                       |

### Guild Join Request Create Dispatch Event

Sent when a guild join request is created such as when joining a server with a verification gate. Structure appears to be the same as [Guild Join Request Update Dispatch Event](#guild-join-request-update-dispatch-event)

### Guild Join Request Update Dispatch Event

Sent when a guild join request is updated such as when accepting rules through the verification gate

| Field    | Type                                                  |                                |
|----------|-------------------------------------------------------|--------------------------------|
| status   | string                                                | see `application_status` above |
| guild_id | snowflake                                             | the guild the request is from  |
| request  | [guild application object](#guild-application-object) | the new request                |

### Guild Join Request Delete Dispatch Event

Sent when a request is deleted such as when leaving a server before completing the verification gate

| Field    | Type      |                              |
|----------|-----------|------------------------------|
| user_id  | snowflake | user who created the request |
| guild_id | snowflake | guild the request is for     |
