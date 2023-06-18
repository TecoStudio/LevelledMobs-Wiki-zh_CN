```
This page was last updated for LevelledMobs 3.8.1 b718
```

***

# Conditions:

These represent the many various checks available against an entity before any **Strategies** or **Apply-Settings** are applied.
**NOTICE**: Your default `rules.yml` file may not include every potential `condition`, `strategy`, or `apply-settings`, so check the wiki regularly for any new updates!

You can refer to the 'last updated' message above to know when this page was last altered. 

```yml
conditions:
  allowed-spawn-reasons:
  allowed-worldguard-regions:
  allowed-worldguard-region-owners:
  apply-above-y: 62
  apply-below-y: 62
  apply-plugins:
  biomes:
  custom-names:
  chance: 1.0
  entities:
  maxLevel: 50
  minLevel: 1
  max-distance-from-spawn: 100
  min-distance-from-spawn: 100
  mob-customname-status: EITHER
  mob-tamed-status: EITHER
  mythicmobs-internal-names:
  permission:
  spawner-names:
  scoreboard-tags:
  stop-processing: true
  within-coordinates:
    start-x: 
    end-x:
    start-y:
    end-y:
    start-z:
    end-z:
  worlds:
  world-time-tick:
  cooldown-duration:
  cooldown-limit:

  level-plugins:
    DANGEROUS_CAVES: false
    ECO_BOSSES: false
    MYTHIC_MOBS: false
    ELITE_MOBS: false
    ELITE_MOBS_NPCS: false
    ELITE_MOBS_SUPER_MOBS: false
    INFERNAL_MOBS: false
    CITIZENS: false
    SHOPKEEPERS: false
    SIMPLE_PETS: false
```

|Config Line Option|Description
|:-:|:---
|`minLevel:`<br />`maxLevel:`|These particular config options are specifically checking for a level AFTER LM has calculated the level of the entity.<br />**Example:** a transforming entity, such as a zombie villager to a regular zombie; or for applying `use-droptable-id:` to entities based on their level or other conditions within the Rules system rather than the CustomDrops system.
|`chance:`|This represents the percent chance of a Custom Rule occurring. It will otherwise be skipped.<br />**Example:** setting `chance: 0.5` would result in a 50% chance.
|`stop-processing:`|This represents a forced stop on the processing of the queued stack of Custom Rules. Once a rule has trigged which contains this config line option, it will prevent any future Custom Rules from being processed.
|`mob-customname-status:`<br />`mob-tamed-status:`|These config options represent a check against whether an entity has a set CustomName or has been tamed:<br />`NOT_SPECIFIED` - The Default status, essentially not checked or utilized<br />`EITHER` - The entity's CustomName or tamed status does not matter<br />`NAMETAGGED` / `TAMED` - The entity needs to have a CustomName or be tamed<br />`NOT_NAMETAGGED` / `NOT_TAMED` - The entity needs to NOT have a CustomName or NOT be tamed
|`worlds:`|A `MODALLIST` config option; this represents a check against the world where the entity spawned.
|`apply-above-y:`<br />`apply-below-y:`|This checks whether the entity is above or below a specific Y coordinate.
|`world-time-tick:`|A `MODALLIST` config option; this represents a check against the current time of day in the world, represented by ticks. A 24 hour day in Minecraft is represented by a world-tick value between `0-24000`. You can get a [better sense of the time of by by referencing this link](https://minecraft.fandom.com/wiki/Daylight_cycle#24-hour_Minecraft_day).
|`min-distance-from-spawn:`<br />`max-distance-from-spawn:`|This checks whether the entity is within a specific minimum or maximum distance from the spawn coordinates.
|`allowed-worldguard-regions:`|A `MODALLIST` config option; this represents a check against the WorldGuard region where the entity spawned.
|`allowed-worldguard-region-owners:`|A `MODALLIST` config option; this represents a check against the owner list of a WorldGuard region where the entity spawned.
|`allowed-spawn-reasons:`|A `MODALLIST` config option; this represents a check against possible spawn reason flags.<br />You can reference [the SpigotMC javadocs](https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/event/entity/CreatureSpawnEvent.SpawnReason.html) regarding `CreatureSpawnEvent.SpawnReason` for the different options.
|`custom-names:`|A `MODALLIST` config option; this represents a check against an entity's CustomName when a level is freshly applied, presuming it has one.
|`entities:`|A `MODALLIST` config option; this represents the entities which the Custom Rule would apply to.
|`biomes:`|A `MODALLIST` config option; this represents a check against the biome where the entity spawned.
|`mythicmobs-internal-names:`|A `MODALLIST` config option; this represents a check against the internal names for MythicMob's custom mobs.<br />**NOTE:** We have experienced several reported issues with establishing compatibility with **MM5** specifically. We are awaiting a solution from the **MM** team. In the meantime, we would recommend sticking with versions of **MM** prior to **5.0.0** until this is resolved.
|`apply-plugins:`|A `MODALLIST` config option; this represents a check against whether the spawned entity came from an internally supported plugin.
|`level-plugins:`|Functions in a similar fashion to `apply-plugins:` above, utilizing a different format used in Default Rules for convenience (though they are interchangeable).
|`scoreboard-tags:`| A `MODALLIST` config option; if a mob contains scoreboard tags, you can use this to include or exclude them.
|`spawner-names:`| A `MODALLIST` config option; this represents a check against the name of the `LM Spawner` which created the entity.
|`permission:`|A `MODALLIST` config option; this represents a check against the nearest player to the entity, OR the player who killed an entity, depending on it's implementation. All permissions as registered as `levelledmobs.permission.<node>`, where `<node>` represents the value of this config. For example, if your permission was `levelledmobs.permission.vip`, you would configure it as such: `permission: ['vip']`.
|`cooldown-duration:`| When configured and the rule is utilized, it will effectively disable the rule until the cooldown time expires.
|`cooldown-limit:`| When a `cooldown-duration:` is configured, this is the number of times the rule must be executed before it becomes disabled for a time.
|`within-coordinates:`<br />`start-` `end-`|This system allows you set the `start-` and `end-` coordinates to define a region within your world to apply a rule within. You can just specify a single axis to mark a single point or line; specify two axis to make a square along those two axis; or specify three to make a cuboid region. You can also place `'-'` or `'+'` as the `end-` of any coordinate and it will go from the `start-` value to infinity in the direction specified. Finally, if you specify a `start-` but do not specify an `end-`, then the `end-` will be the same value as the `start-`; and vice versa. 

***