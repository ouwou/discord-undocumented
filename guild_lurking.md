### Guild Lurking

Guilds with the feature `PREVIEW_ENABLED` can be "lurked" in/previewed before actually joining. This is basically the same as joining except you are granted no permissions and are not counted as a member

#### Start Lurking

PUT `/guilds/{guild.id}/members/@me?lurker=true&session_id={session.id}`  
Session ID is presumably the one found in the READY gateway message and you will be removed when this session expires  
Returns a [guild object](https://discord.com/developers/docs/resources/guild#guild-object)

#### Stop Lurking

Same as [Leave Guild](/join_leave_guild#leave-guild)
