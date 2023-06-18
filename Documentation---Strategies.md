```
This page was last updated for LevelledMobs 3.10.1 b759
```

***

# Strategies:

> ## Distance from Spawn Levelling & Blended Levelling
> This strategy describes 'Distance from Spawn' and 'Blended' Levelling.
> 
> ```yml
> strategies:
>   distance-from-spawn:
>     increase-level-distance: 150
>     start-distance: 250
>     spawn-location:
>       x: default
>       z: default
>     blended-levelling:
>       enabled: false
>       transition-y-height: 62
>       lvl-multiplier: 0.05
>       multiplier-period: 10
>       scale-downward: true
> ```
> ### Here are the formulae used when calculating the Blended Levelling value.<br />The 'postResult' is the final result applied to the entity.<br />
> preResult = (((( transition-y-height: - entityYCoordinate ) / multiplier-period: ) x lvl-multipler: ) x distanceFromSpawnLevel )<br />
> postResult = ( round( preResult ) + distanceFromSpawnLevel )

|Config Line Option|Description
|:-:|:---
|`distance-from-spawn:`|This enables the levelling system.
|`increase-level-distance:`|This represents the number of blocks before the next level increase occurs.
|`start-distance:`|This represents the number of blocks from spawn before the `increase-level-distance:` begins counting.
|`spawn-location:`  `x:`  `z:`|This allows you to adjust the 'spawn' location which LM utilizes for this feature.<br />By leaving it as `default`, it will use your world's set spawn coordinates. You can change this by adjusting the X and Z coordinates.
|`blended-levelling:`  `enabled:`|This system represents the start of the **Blended Levelling** addon to **Distance from Spawn** levelling. This is not it's own levelling system, but rather an attachment to the Distance from Spawn system. When this is enabled, it will continue to use your Distance from Spawn levelling for any entities spawned at `transition-y-height:`.<br />Based on the default settings, any entities which spawn at a higher Y-Coordinate will have their level decrease, while those spawned further underground will increase in level, in relation to the current Spawn Distance level.
|`transition-y-height:`|This represents the Y-coordinate where Spawn Distance Levelling would apply exactly, and where the transition line between a level increase or decrease trend would occur.
|`lvl-multiplier:`|This represents the multiplier applied to the expected Spawn Distance level, applied exponentially every `multiplier-period:` in both directions from the `transition-y-height:`. If the `multiplier-period:` is low, or the `lvl-multiplier:` is high, then entities will increase or decrease in levels at faster rates as you go further from spawn and the multiplier continues to multiply.
|`multiplier-period:`|This represents the number of blocks from the `transition-y-height:` before a `lvl-multiplier:` is applied.
|`scale-downward:`|This setting will determine in what direction the levels would increase from the `transition-y-height:`. When set to `true`, any entity spawned below this transition line will have a positive level multiplier applied, while those above the transition will have a negative multiplier. If this is set to false, then the reverse is true.

***

> ## Y-Coordinate Levelling
> This strategy enables 'Y-Coordinate' Levelling.
> 
> ```yml
> strategies:
>   y-coordinate:
>     start: 100
>     end: 20
>     period: 0
> ```

|Config Line Option|Description
|:-:|:---
|`y-coordinate:`|This enables the levelling system.
|`start:`|This represents the starting Y-Coordinate; where entities are the lowest level.
|`end:`|This represents the ending Y-Coordinate; where entities are the highest level.
|`period:`|Any value in this position other than `0` will override the 'end:' config option. It will instead count the number of blocks in increments of this value beginning from the 'start:' Y-Coordinate, increasing the mobs' level every 'period:' of blocks in the direction of the void.

***

> ## Weighted-Random Levelling
> This strategy enables 'Weighted Random' Levelling.
> 
> ```yml
> strategies:
>   weighted-random: true
> # OR
>   weighted-random:
>     1-2: 5
>     3-4: 4
>     5-6: 3
>     7-8: 2
>     9-10: 1
>     lvl-lvl: chance
> ```
> **Example:** You may simply set `weighted-random: true` and it will use the `minLevel:` and `maxLevel:` to generate a weighted random, where the lowest levels are the most likely to appear, while the highest are least likely.
> 
> **Example:** The above weighted random will generate a list of numbers, using the 'weight' value listed on the right to increase or decrease the chance of the level being randomly selected.<br />1, 1, 1, 1, 1, 2, 2, 2, 2, 2, 3, 3, 3, 3, 4, 4, 4, 4, 5, 5, 5, 6, 6, 6, 7, 7, 8, 8, 9, 10

|Config Line Option|Description
|:-:|:---
|`weighted-random:`|This enables the levelling system. If `weighted-random: true` is used, do not set any custom tiers.
|`lvl-lvl`|These represent the level ranges which will have their own weights applied.
|`chance`|These represent the chance of the preceding level range being used to apply a level. The lower the number, the least likely, when compared to the others.

***

> ## True Random Levelling / Lower Level Bias Factor
> This strategy enables 'True Random' Levelling.
> 
> ```yml
> strategies:
>   random: true
>   lower-mob-level-bias-factor: 5
> ```

|Config Line Option|Description
|:-:|:---
|`random:`|This enables the levelling system.
|`lower-mob-level-bias-factor:`|These will apply a similar effect to the weighted random levelling strategy, but with far less control. The only applicable values here are `0-9`.

***

# Strategy Modifications:

> ## Player Variable Modifier
> This level modifier has special settings located within the `settings.yml` file.
[Check here for details](https://github.com/lokka30/LevelledMobs/wiki/Documentation---settings.yml#player-levelling-strategy-settings)!<br />By default, entities will update every five seconds based on the nearest player within 250 RAYTRACED distance.
> 
> This strategy enables 'Player Variable Level Modification'.
> 
> ```yml
> strategies:
>   player-levelling:
>     match-level: false
>     use-player-max-level: false
>     player-level-scale: 1.0
>     level-cap: 30
>     decrease-level: true
>     recheck-players: false
>     preserve-entity: 10s
>     enabled: true
>     merge: false
>     tiers:
>       1-15: 1-10
>       16-30: 11-20
>       31-45: 21-25
>       v1-v2: lvl-lvl
>     variable: '%level%'
> ```

|Config Line Option|Description
|:-:|:---
|`player-levelling:`|This enables the c. When enabled, this will change the entity levels based on a specified variable from the nearest player.
|`match-level:`|This will cause the entity to use a randomly selected value between 1 and the current `variable:` value of that player.<br />**Example:** While using `%level%`, if I am LVL 30, all entities that adjust their level based on my own will be a randomly selected value between `1-30`.<br>NOTE: When set to true, tiers are not utilized
|`use-player-max-level:`|This will cause the entity to match the current `variable:` value of that player.<br />**Example:** While using `%level%`, if I am LVL 30, all entities that adjust their level based on my own will be `30`.<br>NOTE: When set to true, tiers are not utilized
|`player-level-scale:`|This will adjust the value produced by the `variable:`, multiplying the variable by this value. This is useful for exceptionally large numbers which can be scaled down with a smaller value, or very small numbers which can be scaled upwards.
|`level-cap:`|This sets a hard limit on how high an entity can achieve using this `Player Variable Level Modifier`. This is useful to prevent entities outside of an approved range.
|`decrease-level:`|This setting, when set to `false`, will prevent entities from receiving a level lower than any previously applied by Player Levelling. The entity will continue to potentially be relevelled, however if the newly generated level is lower than the current level, then the change is dropped.
|`recheck-players:`|When set to `true`, this setting will recheck the last player to update an entity, rather than skip that player as it would do normally.
|`preserve-entity:`|This setting will prevent an entity from updating via Player Levelling if it has received damage in the last X time, defaulted to `10s`.
|`enabled:`|You can enable or disable player levelling with this option. Defaults to true.
|`merge:`|If you define multiple rules using player levelling then only the last one will be used. If you set merge to true then the tiers will be added together and some options can be merged together.
|`tiers:`|This represents the logic behind how this system applies levels to entities. The values on the left, marked as `v1` and `v2` in the config above, represent the min and max range of whatever value is listed in the `variable:` config.<br />**Example:** While using `%level%`, if the player was LVL 10, then it would fit within the first variable range of `1-15`, which means it will then apply a random level between the values on the right, marked as `lvl-lvl`.
|`variable:`|This can be one of LevelledMob's built-in variables or represents any dynamic [**PAPI (PlaceholderAPI)**](https://www.spigotmc.org/resources/placeholderapi.6245/) tag, plus a few built in, which will be the variable used when constructing the levels of entities. There should be no limits to this system, so long as the final result of the `variable:` is numeric.<br />Through **PAPI**, you can use a specialized **MATH** feature to even further expand on this system. Simply perform `/papi ecloud download Math` from the console or in-game and it will download the necessary add-on for **PAPI**. To learn how to use this unique system, [click here for the developer's github regarding the add-on and how to use it](https://github.com/Andre601/Math-Expansion).<br>Built-in variables provided by LevelledMobs: %level%, %exp%, %exp-to-level%, %total-exp%, %world_time_ticks%, %bed_distance%, %home_distance%, %home_distance_with_bed%

***

> ## Level Variance Modifier
> 
> ```yml
> strategies:
>   max-random-variance: 2
> ```

Once an entity has received a final level value from other `strategies:`, this `Level Variance Modifier` will apply a random plus or minus value to the level based on the value of the config option listed above.

***