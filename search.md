### Search Messages

GET `/guilds/{guild.id}/messages/search`  
Returns [search results object](#search-results-object) or a 202 Accepted with response code 110000 (Index not yet available. Try again later) if the guild is not indexed  
GET parameters:

| Field       | Type      | Description                                          |
|-------------|-----------|------------------------------------------------------|
| content     | string    | term to search for                                   |
| offset?     | integer   | offset into search results                           |
| channel_id? | snowflake | channel to restrict search to                        |
| author_id?  | snowflake | author to restrict search to                         |
| mentions    | snowflake | restrict search to mentions of given user            |
| has         | string    | "link", "embed", or "file"                           |
| max_id      | snowflake | maximum id of the search results. used for `before:` |
| min_id      | snowflake | minimum id of the search results. used for `after:`  |
| sort_by?    | string    | relevance or timestamp                               |
| sort_order? | string    | desc or asc                                          |

#### Search Results Object

| Field           | Type                                                                                             | Description                    |
|-----------------|--------------------------------------------------------------------------------------------------|--------------------------------|
| analytics_id(?) | string                                                                                           | unknown                        |
| messages        | array of [message objects](https://discord.com/developers/docs/resources/channel#message-object) | messages matching search query |
| total_results   | integer                                                                                          | total number of matches        |
