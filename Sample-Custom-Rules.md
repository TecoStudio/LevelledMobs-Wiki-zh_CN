```
This page was last updated for LevelledMobs 3.9.0 b726
```

***

# Sample Custom Rules

Below are examples of different custom rules which you can apply to your own file for different unique effects! These are just the skeletons, so feel free to modify them to your liking. Almost anything is possible if you can imagine it!

***

> ### Custom Ender Dragon Levelling
> ```yaml
>   - enabled: false
>     name: 'CR - Ender Dragon Fight'
>     use-preset: average_challenge
>     conditions:
>       worlds:
>         allowed-list: ['world_the_end']
>       entities:
>         allowed-list: ['ENDER_DRAGON']
>     apply-settings:
>       minLevel: 25
>       multipliers:
>         custom-mob-level:
>           ENDER_DRAGON:
>             max-health: 3.0
>             attack-damage: 1.0
> ```
> Once enabled, utilizing the preset `average_challenge`, limiting the rule to both the `world_the_end` and the `ENDER_DRAGON` itself. This tells the Ender Dragon to use a `minLevel: 25`, which when using the `average_challenge`, is considered the `maxLevel:` as well. Then we apply custom multipliers specifically for the `ENDER_DRAGON`, adjusting it's `max-health:` and `attack-damage:`, while still utilizing the default multipliers set in the `average_challenge` preset, along with any potential tiered coloring required.

***

> ### Boss-Bar Style Nametag using Health Indicators
> ```yml
>   - enabled: false
>     name: 'CR - Boss Bar'
>     use-preset: allowed_worlds, nametag_using_indicator
>     apply-settings:
>       health-indicator:
>         scale: 2
>         max: 10
>       nametag: '%health-indicator%'
> ```
> Once enabled, this will alter the `nametag:` of an entity to display only the `health-indicator:` style. This custom rule uses the presets to specify both the `allowed_worlds` and collect the coloring and indicator details from `nametag_using_indicator`. This rule will work with any difficulty setting, however it does assume that you are using the `average_challenge` when setting the `scale:`. Using LM's default difficulty settings, it would be recommended to use a `scale: 1` for `basic_challenge` and `scale: 4` for `advanced_challenge`.

***

> ### Night Time Difficulty Increase
> ```yml
>   - enabled: false
>     name: 'CR - Difficulty Increase at Night'
>     use-preset: allowed_worlds, advanced_challenge
>     conditions:
>       apply-above-y: 62
>       world-time-tick: ['13000-24000']
>     apply-settings:
>       minLevel: 25
> ```
> Once enabled, this will increase the difficulty of the entities spawned at night, from the onset of night to the cusp of dawn. This also only applies to the entities above `y=62` so that those entities might die when the sun comes up. This also restricts those entities to a level between `25-50`, based on the default settings for the `advanced_challenge` preset.

***

> ### Deny Levelling in Specific Biomes
> ```yml
>   - enabled: false
>     name: 'CR - NoLevel Biomes'
>     conditions:
>       worlds:
>         allowed-list: ['world_nether']
>       biomes:
>         allowed-list: ['NETHER_WASTES']
>     apply-settings:
>       maxLevel: 0
> ```
> Once enabled, this custom rule will prevent entities from levelling when located within the `world:` `world_nether`, and the `biome:` `NETHER_WASTES`. A simple and easy to implement rule!

*** 

> ### Customized Entity Name Based On Level
> ```yml
>   - enabled: false
>     name: 'CR - Level Dependent Zombie Custom Names'
>     use-presets: allowed_worlds
>     apply-settings:
>       entity-name-override:
>         1-5:
>           ZOMBIE: ['Teething %displayname%']
>         6-10:
>           ZOMBIE: ['Scratching %displayname%']
>         11-20:
>           ZOMBIE: ['Biting %displayname%']
>         21-25:
>           ZOMBIE: ['Hunting %displayname%']
>         BABY_ZOMBIE: ['Baby Undead']
> ```
> Once enabled, this custom rules uses a special feature of the `entity-name-override:` which allows you to specify the level range which a custom name would apply. This scale presumes you are using the `average_challenge` preset, but all can be adjusted! You can also add conditions, such as biome limitations, which would allow you to further customize!

*** 

> ### Nerfed Spawner Cube Entities
> ```yml
>   - enabled: false
>     name: 'CR - Nerfed Spawner Cubes'
>     priority: 1
>     use-preset: allowed_worlds
>     conditions:
>       allowed-spawn-reasons:
>         allowed-list: ['SPAWNER']
>     apply-settings:
>       entity-name-override:
>         all_entities: 'Spawned %displayname%'
>       multipliers:
>         max-health: 0.0 # For Farming
>         armor-bonus: 0.0
>         armor-toughness: 0.0
>         xp-drop: 0.0
> ```
> Once enabled, this custom rules will level entities that are generated from Spawner Cubes the same as any other on the server, except for their health not changing (their damage will still increase!). This also adds the `Spawned ` prefix to their names, making them easier to locate. 

*** 

> ### NBT-API | Startled Creepers!
> ```yml
>   - enabled: false
> #   This rule requires the soft-dependency NBT-API to function!
> #   Make sure you have it installed prior to enabling this rule!
>     name: 'CR - NBT - 20% Startled Creepers, Short Fuse'
>     use-preset: allowed_worlds
>     conditions:
>       chance: 0.2
>       entities:
>         allowed-list: ['CREEPER']
>     apply-settings:
>       nbt-data: '{Fuse:2,Attributes:[{Name:"generic.follow_range",Base:1f}]}'
>       entity-name-override:
>         CREEPER: ['Startled %displayname%']
> ```
> This custom rule requires the soft-dependency NBT-API to function!
> Once enabled, this rule will apply `nbt-data:` to the `CREEPER` entity. This applies at a `chance: 0.2`, or 20%. It will also change the Creeper's name to `Startled Creeper`, distinguishing them from normal `CREEPER`'S.
> The `nbt-data:` listed will adjust the `CREEPER`'S fuse duration to half a second, and make it so that they can not see the player until they are within about two blocks from them. This is where the concept of a 'startled' creeper came about!

***

> ### Using Drop-Tables with Custom Rules
> ```yaml
>  - enabled: true
>    name: 'Drop Tables for LVL1-12'
>    conditions:
>      entities:
>        allowed-list: ['ZOMBIE', 'SKELETON', 'HUSK', 'DROWNED']
>      minLevel: 1
>      maxLevel: 12
>    apply-settings:
>      use-droptable-id: basic_weapons_table, basic_armor_table
>
>  - enabled: true
>    name: 'Drop Tables for LVL13-24'
>    conditions:
>      entities:
>        allowed-list: ['ZOMBIE', 'SKELETON', 'HUSK', 'DROWNED']
>      minLevel: 13
>      maxLevel: 24
>    apply-settings:
>      use-droptable-id: average_weapons_table, average_armor_table
>
>  - enabled: true
>    name: 'Drop Tables for LVL25'
>    conditions:
>      entities:
>        allowed-list: ['ZOMBIE', 'SKELETON', 'HUSK', 'DROWNED']
>      minLevel: 25
>    apply-settings:
>      use-droptable-id: extreme_weapons_table, extreme_armor_table
> ```
> You can use the `use-droptable-id:` system as an `apply-settings:` config option which will allow you to build a loot table within the `customdrops.yml` file, and then set any number of `conditions:` within the Rules system to apply these tables in a more unique way than what the Custom Drops system can provide alone.

***

> ### Using Custom Variables with Placeholder API (PAPI) and Player Level Modifier
> ```yaml
>  - enabled: true
>    name: 'Player Level Modifier using Statistic and Math Modules'
> #  This rule requires the soft-dependency PlaceholderAPI to function!
> #  Make sure you have it installed prior to enabling this rule!
>    strategies:
>      player-levelling:
>        match-level: true
>        use-player-max-level: false
>        decrease-level: true
>        player-level-scale: 1.0
>        level-cap: 25
>        tiers:
>          1-15: 1-10
>          16-30: 11-20
>          31-45: 21-25
>        variable: '%math_({statistic_damage_dealt}-({statistic_damage_taken}*5))/1000%'
> ```
> This system allows you to modify an entities' level based on some variable produced by the nearest player to the entity. By default this is the vanilla Minecraft level of the player, however in this example we combine two PlaceholderAPI modules to produce higher entity levels when the player deals more damage, and will reduce the level if the player begins to take damage. To use the `variable:` above, after downloading and installing PlaceholderAPI, you need to perform `/papi ecloud download Math`, `/papi ecloud download Statistic`, and then `/papi reload` to access those modules.
> 
> This version of this variable states that it will take the damage the player deals to mobs, subtract five times the amount of damage that the player has received from any source, and then divide that total by 1000. This produces a small number which will grow gradually over time if the player deals out the damage, but will reduce itself more if the player begins to take damage.

***

> ### The Average Challenge; Using Stacked Multipliers
> ```yaml
>   - enabled: true
>     name: 'Average-Challenge Stacked Multipliers'
>     apply-settings:
>       minLevel: 1
>       maxLevel: 25
>       multipliers:
> #       use-stacked: true
>         max-health: ['4.25', 'STACKED']
>         movement-speed: ['0.002', 'STACKED']
>         attack-damage: ['0.25', 'STACKED']
>         ranged-attack-damage: ['0.25', 'STACKED']
>         creeper-blast-damage: ['0.03', 'STACKED']
>         item-drop: ['0.25', 'STACKED']
>         xp-drop: ['17.5', 'STACKED']
> ```
> This is a modification of the multiplier system which would instead stack the multipliers per level rather than use the default percentage formula. Using `['X', 'STACKED']`, you can set the stacked value for that specific multiplier while letting the others use the default system; or you can enable `use-stacked:` and it will activate for all entries beneath it.

***

> ### Using %world_time_ticks% with Player Level Modifier
> ```yaml
>  - enabled: true
>    name: 'Player Level Modifier with World Time Tick'
>    strategies:
>      player-levelling:
>        match-level: false
>        use-player-max-level: false
>        decrease-level: true
>        player-level-scale: 1.0
>        level-cap: 25
>        recheck-players: true
>        preserve-entity: 10s
>        tiers:
>          0-1000: 13-19  # Sunrise
>          1000-2000: 11-17
>          2000-3000: 9-15
>          3000-4000: 7-12
>          4000-5000: 5-9
>          5000-6000: 2-7
>          6000-7000: 1-5  # Noon
>          7000-8000: 2-7
>          8000-9000: 5-9
>          9000-10000: 7-12
>          10000-11000: 9-15
>          11000-12000: 11-17
>          12000-13000: 13-19  # Sunset
>          13000-14000: 15-21
>          14000-15000: 17-23
>          15000-16000: 19-25
>          16000-17000: 21-25
>          17000-18000: 23-25
>          18000-19000: 25-25  # Midnight
>          19000-20000: 23-25
>          20000-21000: 21-25
>          21000-22000: 19-25
>          22000-23000: 17-23
>          23000-24000: 15-21
>        variable: '%world_time_ticks%'
> ```
> This Player Level Modifier will use an internal placeholder called `%world_time_ticks%` as the `variable:`, and the `tiers:` are arranged so that the level becomes easier during the day centered on noon, and more difficult during at night centered on midnight. The levels are based on the `average_challenge`.

***

> ### Creating 'rings' of levels centered from spawn
> ```yaml
>  - enabled: true
>    name: 'Level 1-5 Ring'
>    conditions:
>      min-distance-from-spawn: 200
>      max-distance-from-spawn: 1000
>    strategies:
>      weighted-random: true
>    apply-settings:
>      maxLevel: 5
> 
>  - enabled: true
>    name: 'Level 5-10 Ring'
>    conditions:
>      min-distance-from-spawn: 1000
>      max-distance-from-spawn: 2000
>    strategies:
>      weighted-random: true
>    apply-settings:
>      minLevel: 5
>      maxLevel: 10
> ```
> This pair of custom rules demonstrate the principal of creating 'rings' of levels centered around the spawn. While this is similar to Spawn Levelling, this method creates rings of influence with distinct regions rather than a gradual progression.