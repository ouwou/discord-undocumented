# Remote Auth (QR Code Login)

Remote auth lets you log into Discord on desktop by scanning a QR code on your phone.

On desktop, Discord firsts open a WebSocket connection to `REMOTE_AUTH_ENDPOINT`, currently `wss://remote-auth-gateway.discord.gg/?v=2`

???+ info
     Unlike the normal Discord gateway, data fields do not belong to a `d` sub-object; all fields are at the top level, next to `op`. For example, the `hello` opcode looks like this:
     ```json
     {
         "op": "hello",
         "timeout_ms": 123456,
         "heartbeat_interval": 41250
     }
     ```

On open, the gateway sends opcode `hello`.

## `hello`

| Field | Type | Description |
|-------|------|-------------|
| timeout_ms | integer | milliseconds until the client should disconnect with `4003 Handshake Timeout` |
| heartbeat_interval | integer | milliseconds interval for sending `heartbeat` ops |

When the desktop receives `hello`, it uses the SubtleCrypto interface to generate a 2048-bit RSA key and encodes the public key in SubjectPublicKeyInfo format.

The desktop then sends an opcode `init`.

## `init`

| Field | Type | Description |
|-------|------|-------------|
| encoded_public_key | string | base64-encoded public key |

The gateway responds with opcode `nonce_proof`.

## `nonce_proof` (Server to client)

| Field | Type | Description |
|-------|------|-------------|
| encrypted_nonce | string | base64-encoded encrypted nonce |

The desktop decrypts it with its private key using OAEP and sends back a `nonce_proof`.

## `nonce_proof` (Client to server)

| Field | Type | Description |
|-------|------|-------------|
| nonce | string | base64-encoded decrypted nonce |

The gateway responds with `pending_remote_init` and then the next stop involves scanning the QR code.

## `pending_remote_init`

| Field | Type | Description |
|-------|------|-------------|
| fingerprint | string | |

The QR code is generated using the string `https://discord.com/ra/{fingerprint}`.

When a mobile device scans the QR code, it extracts the fingerprint from the url and makes a REMOTE_AUTH_INITIALIZE request.

## REMOTE_AUTH_INITIALIZE

### POST `/users/@me/remote-auth`

| Field | Type | Description |
|-------|------|-------------|
| fingerprint | string | fingerprint from the QR code |

Return value:

| Field | Type | Description |
|-------|------|-------------|
| handshake_token | string | temporary token to finalize login |

After the mobile device makes this request, the remote auth gateway sends a `pending_ticket` to the desktop.

## `pending_ticket`

| Field | Type | Description |
|-------|------|-------------|
| encrypted_user_payload | string | encrypted user payload described below |

### Encrypted user payload

`<user id>:<discriminator>:<avatar hash>:<username>`

The mobile device then confirms the login request with a REMOTE_AUTH_FINISH request.

## REMOTE_AUTH_FINISH

### POST `/users/@me/remote-auth/finish`

| Field | Type | Description |
|-------|------|-------------|
| handshake_token | string | token from REMOTE_AUTH_INITIALIZE |
| temporary | boolean | false |

After the mobile device sends a REMOTE_AUTH_FINISH, the gateway sends a `pending_login` to the desktop and the websocket is closed.

## `pending_login`

| Field | Type | Description |
|-------|------|-------------|
| ticket | string | ticket to use for obtaining the token |

## REMOTE_AUTH_LOGIN

After getting the ticket, the desktop makes one last request to get the token

### POST `/users/@me/remote-auth/login`

| Field | Type | Description |
|-------|------|-------------|
| ticket | string | ticket from `pending_login` |

Response:

| Field | Type | Description |
|-------|------|-------------|
| encrypted_token | string | encrypted token, decrypted like everything else |

## REMOTE_AUTH_CANCEL

The mobile device can cancel a pending remote auth login by sending a REMOTE_AUTH_CANCEL. The desktop receives a `cancel` event.

### POST `/users/@me/remote-auth/cancel`

| Field           | Type   | Description                       |
|-----------------|--------|-----------------------------------|
| handshake_token | string | token from REMOTE_AUTH_INITIALIZE |

## `cancel`

Received when the mobile devices cancels a login request. There is no extra data for this op.
