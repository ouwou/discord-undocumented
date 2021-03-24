### Account Verification

When Discord thinks you might be a spammer or doing something naughty it will send `USER_REQUIRED_ACTION_UPDATE` as described below

#### User Required Action Update Dispatch Event

| Field           | Type   | Description                        |
|-----------------|--------|------------------------------------|
| required_action | string | type of required action. see below |

#### Required Action Type

| Name                   | Description                          |
|------------------------|--------------------------------------|
| REQUIRE_CAPTCHA        | user must complete a captcha         |
| REQUIRE_VERIFIED_EMAIL | user must verify an email            |
| REQUIRE_VERIFIED_PHONE | user must verify with a phone number |

#### Send Phone Verification Code

POST `/users/@me/phone`  
Returns 204 No Content on success
JSON parameters:

| Field | Type   | Description                          |
|-------|--------|--------------------------------------|
| phone | string | phone number in format "+1234567890" |

Errors:

| Error | Description          |
|-------|----------------------|
| 50022 | Invalid phone number |

#### Verify Phone with Code

POST `/phone-verifications/verify`  
Returns 400 Bad Request on bad code or 200 OK on success  
JSON parameters:

| Field | Type   | Description                          |
|-------|--------|--------------------------------------|
| code  | string | the verification code                |
| phone | string | phone number in format "+1234567890" |

Return object:

| Field | Type   | Description                         |
|-------|--------|-------------------------------------|
| token | string | token used to finalize verification |

#### Finalize Phone Verification

POST `/users/@me/phone`  
Returns 204 No Content on success  
JSON parameters:

| Field       | Type   | Description                                                           |
|-------------|--------|-----------------------------------------------------------------------|
| password    | string | account password                                                      |
| phone_token | string | token received from [Verify Phone with Code](#verify-phone-with-code) |
