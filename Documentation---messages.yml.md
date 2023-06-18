```
This page was last updated for LevelledMobs 3.1.1 b481
```

***

# Messages Configuration

## About:
LevelledMobs' `messages.yml` file allows you to customise all of the chat messages that are sent from the plugin.

## Placeholders:

LevelledMobs allows you to include a bunch of different placeholders in your messages. Placeholders look like `%this%` and are replaced when the message is sent to players.

### Warning:
> **Most placeholders only work in certain messages.**

> Usually, if a placeholder is not included in a message by default, it will not be processed in it.

> For this reason, you may find it useful to reference the default messages.yml file if you are unsure which placeholders are supported in one or more messages in the file.

> For example, you will not be able to use the `%supportedVersions%` placeholder in the 'no permission' message.

### List:

|Config Line Option|Description
|:-:|:---
|`%prefix%`|The prefix LevelledMobs uses before any messages sent via the plugin.
|`%player%`|The name of the player who the event is directed towards.
|`%label%`|The main command alias used when running LM's commands.<br />**Example:** `/lm` or `/levelledmobs`
|`%amount%`|The input value of the event.
|`%entityType%`|The `EntityType` value of the event.
|`%level%`|The level of the entity from the event being processed.
|`%summonType%`|The input value of the summon `EntityType`
|`%entity%`|The nametag, `CustomName`, or default name value of the entity being processed.
|`%x%`  `%y%`  `%z%`|These three tags report back the **X**, **Y**, and **Z** coordinates of the event.
|`%world%`|The value of the world name where the event took place.
|`%targetUsername%`|The username of the target of the event.
|`%targetDisplayname%`|The displayname of the target of the event.
|`%maxAmount%`|Returns the value of the **_Summon Command Limiter_** from `settings.yml`.
|`%minLevel%`  `%%maxLevel%`|Returns the `minLevel` and `maxLevel` value present during the processed event.
|`%killed%`|Returns the number of entities which were killed during the processed event.
|`%skipped%`|Returns the number of entities which were skipped during a LM kill event.
|`%radius%`|The input value of the radius used in LM's summon command.
|`%minRadius%`  `%maxRadius%`|Returns the minimum and maximum radius value.
|`%version%`|Returns the current version of LM, formatted `LM X.Y.Z b000`, where `X.Y.Z` represents the release version and `b000` represents the actual build number.
|`%description%`|Returns the internal LM description text.
|`%supportedVersions%`|Returns the internal LM supported version text.
|`%contributors%`|Returns the internal LM contributors list text.
|`%incompatibilities%`|Returns the internal LM incompatibilities text.