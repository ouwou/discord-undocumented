### Guild Discovery Catalog

#### Get Discovery Categories

GET `/discovery/categories`  
Returns array of [discovery category objects](#discovery-category-object) (unlocalized objects)  
GET parameters:

| Name         | Type   | Description                                   |
|--------------|--------|-----------------------------------------------|
| locale       | string | locale to return. doesn't seem to do anything |
| primary_only | bool   | only return primary-level categories          |

#### Discovery Category Object

| Field       | Type                                              | Description                        |
|------------|----------------------------------------------------|------------------------------------|
| id         | integer                                            | unique id for the category         |
| is_primary | bool                                               | is the category a primary category |
| name       | string or [localized name](#localized-name-object) | name of the category               |

#### Localized Name Object

| Field         | Type                                                   | Description                            |
|---------------|--------------------------------------------------------|----------------------------------------|
| default       | string                                                 | fallback localization string (english) |
| localizations | array of object, key is language code, value is string | localized versions of the string       |

#### Get Discoverable Guilds

GET `/discoverable-guilds`  
Returns [discoverable guilds response object](#discoverable-guilds-response-object)  
GET parameters:

| Name       | Type    | Description                    |
|------------|---------|--------------------------------|
| offset     | integer | offset into the list of guilds |
| limit      | integer | limit of guilds to get         |
| categories | integer | category to limit response to  |

#### Discoverable Guilds Response Object

| Field  | Type                                                                                                                   | Description                     |
|--------|------------------------------------------------------------------------------------------------------------------------|---------------------------------|
| limit  | integer                                                                                                                | limit given in request          |
| offset | integer                                                                                                                | offset given in request         |
| total  | integer                                                                                                                | total number of matching guilds |
| guilds | array of [guild objects](https://discord.com/developers/docs/resources/guild#guild-object) with extra keys (see below) | list of discoverable guilds     |

guilds object extra fields:

| Field                  | Type                                                                        | Description                |
|------------------------|-----------------------------------------------------------------------------|----------------------------|
| keywords               | array of string                                                             | keywords of the guild      |
| primary_category_id(?) | integer                                                                     | id of the primary category |
| categories             | array of localized [discovery category objects](#discovery-category-object) | categories of the guild    |
| auto_removed(?)        | bool(?)                                                                     | unknown                    |

#### Join Discoverable Guild

PUT `/guilds/{guild.id}/members/@me`  
Returns a [guild object](https://discord.com/developers/docs/resources/guild#guild-object)  
The official client also adds the GET parameters `lurker=false` though it's unclear what difference this makes

#### Searching Discoverable Guilds

Discord uses [Algolia](https://algolia.com) with key `NKTZZ4AIZU` to search for guilds which is beyond the scope of this page  
GET `/discovery/valid-term?term={term}` will return `{"valid": true}` if a search term is valid
