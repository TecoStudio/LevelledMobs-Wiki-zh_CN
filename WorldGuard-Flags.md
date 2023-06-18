```
This page was last updated for LevelledMobs 3.2.0 b520
```

***

⚠

**As of LevelledMobs 3.2.0 b511, the WorldGuard flags were removed.**

**We instead exclusively use the `allowed-worldguard-regions:` [condition](https://github.com/lokka30/LevelledMobs/wiki/Documentation---Conditions,-Strategies,-and-Apply-Settings#conditionshttps://github.com/lokka30/LevelledMobs/wiki/Documentation---Conditions,-Strategies,-and-Apply-Settings#conditions) configuration option.**

**This section will be removed at a future date.**

***

Here is a list of WorldGuard flags you can use for your WorldGuard regions - you must have WorldGuard installed if you wish to use these features. Note that WorldGuard is not required to be installed alongside LevelledMobs.

## `LM-AllowLevelledMobs`
Allows you to disable mobs that spawn inside the region from being levelled.

Use `ALLOW` or `DENY`.

By default, this is `ALLOW`.

## `LM-UseCustomLevels`
Tells LM to use the min and max flags you have set (see below).

Use `ALLOW` or `DENY`.

By default, this is `DENY`.

## `LM-CustomMinLevel`
Tells LM what minimum level you want mobs to be that spawn in the region.

Use an integer.

By default, this is `-1` indicating that it is disabled.

## `LM-CustomMaxLevel`
Tells LM what maximum level you want mobs to be that spawn in the region.


Use an integer.

By default, this is `-1`, indiating that it is disabled.