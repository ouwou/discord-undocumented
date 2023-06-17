# Guild Directories

Guild directories are a special type of channel that serve as directories for servers. They are locked behind the
`HUBS` guild feature.

## Get Directory Channel Entries

**GET** `/channels/{channel.id}/directory-entries`

Returns array of [Directory Entry](#directory-entry-object)

## Directory Entry Object

| Field                       | Type                                            | Description                                 |
|-----------------------------|-------------------------------------------------|---------------------------------------------|
| directory_channel_id        | snowflake                                       | id of channel to which the entry belongs(?) |
| entity_id                   | snowflake                                       | id of the guild the entry is for            |
| type                        | [directory entry type](#directory-entry-type)   | the type of the entry                       |
| author_id                   | snowflake                                       | who created the entry                       |
| created_at                  | ISO-8601 timestamp                              | when the entry was created                  |
| description                 | string                                          | description displayed for the entry         |
| name?                       | ?string                                         | name of the entry                           |
| icon?                       | ?string                                         | icon of the entry                           |
| splash?                     | ?string                                         | splash of the guild                         |
| features?                   | ?array                                          | array of guild features                     |
| approximate_member_count?   | ?number                                         | number of members                           |
| approximate_presence_count? | ?number                                         | number of online members                    |

## Directory Entry Type

| Name  | Value |
|-------|-------|
| GUILD | 0     |

## Create Directory Entry

**POST** `/channels/{channel.id}/directory-entry/{entry.id}`

Request body:

| Field       | Type   | Description              |
|-------------|--------|--------------------------|
| description | string | description of the entry |

Creates a new entry for the directory
