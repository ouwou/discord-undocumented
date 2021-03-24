### Managing Guild Discovery and Partnership

#### Get Guild Discovery Requirements

GET `/guilds/{guild.id}/discovery-requirements`  
Returns a [guild requirements object](#guild-requirements-object)

#### Get Guild Partnership Requirements

GET `/partners/{guild.id}/requirements`  
Returns a [guild requirements object](#guild-requirements-object)

#### Guild Requirements Object

| Field                           | Type                                              | Description                                  |
|---------------------------------|---------------------------------------------------|----------------------------------------------|
| age                             | bool                                              | is the guild old enough                      |
| engagement_healthy              | bool                                              | do members visit and talk enough             |
| health_score                    | object, unknown structure                         | unknown                                      |
| health_score_pending            | bool                                              | is waiting on server activity metrics           |
| healthy                         | bool                                              | are server activity requirements met         |
| nsfw_properties                 | [nsfw properties object](#nsfw-properties-object) | channels with meanie words in them           |
| protected                       | bool                                              | is 2FA enabled for moderators                |
| retention_healthy               | bool                                              | is member retention sufficient               |
| safe_environment                | bool                                              | if false, guild was flagged by Trust & Safety |
| size                            | bool                                              | are there enough members in the guild        |
| sufficient                      | bool                                              | are all requirements met                     |
| sufficient_without_grace_period | bool                                              | unknown                                      |
| minimum_age                     | integer                                           | how many days old the guild must be          |
| minimum_size                    | integer                                           | how many members the guild must have         |
| valid_rules_channel             | bool                                              | does the guild have a rules channel          |

#### NSFW Properties Object

| Field    | Type               | Description                      |
|----------|--------------------|----------------------------------|
| channels | array of snowflake | channels with unacceptable names |
