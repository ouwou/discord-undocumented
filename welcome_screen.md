### Welcome Screen

#### Get Welcome Screen

GET `/guilds/{guild.id}/welcome-screen`

Returns a [welcome screen object](https://discord.com/developers/docs/resources/guild#welcome-screen-object-welcome-screen-structure) or 204 No Content if there is none set  

#### Modify Welcome Screen

PATCH `/guilds/{guild.id}/welcome-screen`  
Request body is a [welcome screen object](https://discord.com/developers/docs/resources/guild#welcome-screen-object-welcome-screen-structure)  
Returns a new [welcome screen object](https://discord.com/developers/docs/resources/guild#welcome-screen-object-welcome-screen-structure) on succses  
