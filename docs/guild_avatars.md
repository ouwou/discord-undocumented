# Guild Avatars

Per-server avatars are implemented by adding a new optional/nullable(?) field `avatar` to the guild member object representing a hash like the `avatar` field of the user object.

The asset can be accessed with this URL:

`https://cdn.discordapp.com/guilds/{guild.id}/users/{user.id}/avatars/{hash}.{ext}`

This URL likewise respects the size parameter
