```
This page was last updated for LevelledMobs 3.9.0 b726
```

***

# Apply-Settings:

These represent the many various settings and qualities which are applied utilizing the levelling **strategy** combined with a strong **conditions** check.

```yml
apply-settings:
  baby-mobs-inherit-adult-setting: true
  creature-death-nametag: '%tiered%Lvl %mob-lvl%&8 | &f%entity-name%'
  death-messages:
    1: ['%player% was killed by %death_nametag%!']
  creeper-max-damage-radius: 3
  level-inheritance: true
  maxLevel: 25
  minLevel: 1
  nametag: '&8&l༺ %tiered%Lvl %mob-lvl%&8 | &f%displayname%&8 | &f%entity-health-rounded% %tiered%%heart_symbol% &r%health-indicator% &8&l༻'
  nametag-always-visible-time: 4000
  nametag-placeholder-unlevelled: ''
  nametag-placeholder-levelled: ''
  nametag-visibility-method: ['TARGETED', 'TRACKING', 'ATTACKED']
  nbt-data: ''
  sunlight-intensity: 5
  passenger-match-level: true
  use-custom-item-drops-for-mobs: false
  use-droptable-id: ''
  lock-entity: false

  entity-name-override:
    SKELETON: 'Jack Skellington'
    all_entities: 'Spawner %displayname%'

  entity-name-override:
    LVL-LVL:
      SKELETON: ['Verta Brae', 'Billy Bones']

  health-indicator:
    indicator: '█'
    indicator-half: '▌'
    scale: 4
    max: 5
    colored-tiers:
      tier-1: '&#22E76B' #Green
      tier-2: '&#528CFF' #Blue
      tier-3: '&#FFCD56' #Yellow
      tier-4: '&#FE803C' #Orange
      tier-5: '&#F2003D' #Red
      tier-6: '&#B447FF' #Purple
      tier-#: 'color'
      default: '&#FFFFFF' #White
    merge: true

    multipliers:
#     Stacked Multipliers
      use-stacked: true
      max-health: ['5.0', 'STACKED']
#     All Entities/Default Attributes
      max-health: 5.0
      movement-speed: 0.15
      attack-damage: 2.25
      ranged-attack-damage: 2.0
      creeper-blast-damage: 1.0
      follow-range: 0
      item-drop: 3
      xp-drop: 5
#     Special Multipliers (0.0 Min - 1.0 Max)
      armor-bonus: 0.25
      armor-toughness: 0.15
      attack-knockback: 0.25
      knockback-resistance: 0.2
      zombie-spawn-reinforcements: 0.25

      vanilla-bonus: ['']

      custom-mob-level:
        EntityType:
          max-health: 5.0
          movement-speed: 0.15
          attack-damage: 2.25
          ranged-attack-damage: 2.0
          creeper-blast-damage: 1.0
          item-drop: 3
          xp-drop: 5
    tiered-coloring:
      1-5: '&#22E76B' #Green
      6-10: '&#528CFF' #Blue
      11-15: '&#FFCD56' #Yellow
      16-20: '&#F2003D' #Red
      21-25: '&#B447FF' #Purple
      LVL-LVL: 'color'
      default: '&#FFFFFF' #White

    maximum-death-in-chunk-threshold: 0
    max-adjacent-chunks: 3
    chunk-max-cooldown-seconds: 300
    disable-vanilla-drops-on-chunk-max: false

    spawner-particles: 'SOUL'
    spawner-particles-count: 10
```

> ### Here is the formula used when calculating the Default Multipliers.<br />
> newValue = defaultValue + (( defaultValue x configValue ) x ( entityLevel / maxLevel ))

> ### Here is the formula used when calculating the Special Multipliers.<br />
> newValue = (entityLevel / maxLevel) x (attributeMax x configValue)
> 
> The `attributeMax` is hardcoded to reflect the following, based on the Maximum value possible in-game.
> 
> `armor-bonus:` - 30.0 <br />
> `armor-toughness:` - 20.0 <br />
> `attack_knockback:` - 5.0 <br />
> `knockback_resistance:` - 1.0 <br />
> `zombie-spawn-reinforcements:` - 1.0 

# Hard-Coded Placeholders

Below consists of a list of premade, built-in placeholders which can be used when constructing a `nametag:`.

|Placeholder|Description
|:-:|:---
|`%displayname%`|This represents the killed entity's CustomName field.
|`%health-indicator%`|This represents the health-indicator bar system.
|`%mob-lvl%`|This represents the killed entity's level.
|`%entity-name%`|This represents the killed entity's EntityType.
|`%levelledmobs_killed-by%`|This represents the EntityType of the last entity to kill a player.
|`%death_nametag%`|This represents the value of `creature-death-nametag:`.
|`%entity-health%`|This represents the killed entity's health, exactly.
|`%entity-health-rounded%`|This represents the killed entity's health, rounded to nearest whole exactly.
|`%entity-max-health%`|This represents the killed entity's maximum health, exactly.
|`%entity-max-health-rounded%`|This represents the killed entity's maximum health, rounded to nearest whole number.
|`%heart_symbol%`|This represents the symbol `♥`.
|`%tiered%`|This represents the effective color as selected by `tiered-coloring:`.
|`%wg_region%`|This represents the WorldGuard region where the entity died.
|`%world%`|This represents the world name where the entity died.
|`%location%`|This represents the three coordinate points for the location of the entity's death. The output is as `X Y Z`.

*** 

|Config Line Option|Description
|:-:|:---
|`minLevel:`  `maxLevel:`|These represent the `minLevel` and `maxLevel` to apply to the entity.
|`nametag:`|This represents LM's nametag which hovers over the entity.<br />You must have [**ProtocolLib**](https://www.spigotmc.org/resources/protocollib.1997/) installed for any supported Minecraft 1.16 server for this feature to function.<br />You can disable nametags by changing this value to `disabled`. To make the nametag bar disappear entirely, make sure to change `nametag-visibility-method:` to `disabled` as well.
|`creature-death-nametag:`|This represents the name used whenever a player is killed by a levelled entity.
|`death-messages:`|This represents the beginning of the Death Messages tree, where you define the settings to alter the messages sent to players when they are killed an an entity. You would set the chance of the message being used by changing the number on the left, while including your altered message on the right. This system works similar to the `weighted-random:` level modifier: the higher the number on the left, the higher the chance of that message being used.
|`nametag-visible-time:` `nametag-visibility-method:`|These settings control when and for how long LevelledMobs will display the Nametag for an entity. By default, the three options `TARGETED`, `TRACKING`, and `ATTACKED` are used.<br />`TARGETED` - When an entity has targeted a player with Line of Sight.<br />`ATTACKED` - When a Player attacks an entity.<br />`TRACKING` - When an entity is actively tracking a targeted player (Follow Range).<br />`ALWAYS_ON` - The Nametag remains visible, even through blocks.<br />`MELEE` - The Nametag is only visible in melee range.<br />`DISABLED` - The Nametag is disabled.<br />If the entity's Nametag has been enabled, the timer, measured in milliseconds, will count down until the next activation event, otherwise it will reset the Nametag back to the default configuration.<br />We are working to improve the Nametag system without sacrificing efficiency and resource management. This is the latest step, but we are always looking for the Holy Grail; if you've got a way to improve it, let us know!
|`nametag-placeholder-unlevelled:` `nametag-placeholder-levelled:`|This represents the different potential values for the `%levelledmobs_mob-target%` placeholder. If not populated, the default `nametag:` value will be used.
|`health-indicator:`|This represents the beginning of the Health Indicator system tree, where you define the settings necessary to utilize the `%health-indicator%` tag which can be used within the `nametag:` config option.
|`indicator:`  `indicator-half:`|These two config options represent the character used as an indicator within the Health Indicator system. The `indicator:` is used for most tiers, while the `indicator-half:` is used once the creature has reached the final tier of their health and it begins to wind down to zero.
|`scale:`  `max:`|These two config options adjust how the Health Indicator looks. The `max:` represents how many of the `indicator:` are present in the bar, while the `scale:` represents how many health points each `indicator:` represents. This is also used to determine what tier it is in.
|`colored-tiers:`  `tier-#:`  `default:`  `merge: true`|This represents the different colors of the Health Indicator bar, used to express higher levels of health by using different tiers of colors which change from one to the next as the health changes.<br />Each tier represents a chunk of health calculated as ` 1Tier = ( max: x scale: ) ` and so each subsequent tier represents an additional same chunk of health.<br />**Example:** using a `scale: 4` and `max: 5`, that means each tier is worth `20hp`. If I had an entity which, at max level, would be `110hp`, then that means I would need a minimum of `6` tiers to color every tier of health that could display. Any health that exceeds the available health within the tiers is given the `default:` color. Finally, if you separate your `health-indicator:` settings as we have done in the default configuration file, you can use `merge: true` to bring the two values together.
|`multipliers:`|This represents the beginning of the Multipliers system tree, where you can adjust the change in entity attributes based on their maximum level. This value represents the percent increase of the entity's attribute when at maximum level. By default, we use the multipliers `max-health`, `movement-speed`, `attack-damage`, `ranged-attack-damage`, `creeper-blast-damage`, `follow-range`, `item-drop`, and `xp-drop`. The remaining attributes are special due to the fact that most entities do not spawn with a value in this slot. As we are artificially adding them, we need to use a different formula to apply their attributes, from a `0.0` or 0% of that attribute to a `1.0` or 100% of that attribute. If you are unsure, [refer to this page to see whether your chosen attribute will work](https://minecraft.fandom.com/wiki/Attribute)!
|`multipliers:`  `custom-mob-level:`|This represents the ability to make adjustments to a specific entity's multipliers in a convenient way. This is meant to be a sub-section of `multipliers:` as demonstrated in the above code. Once you select a specific EntityType, ensure you match the necessary formatting, and then use the above listed `multipliers:` to make adjustments to the default applied values.
|`multipliers:`  `use-stacked:` `['X', 'STACKED']`|This system allows you to modify how the multipliers are processed. Instead of the default formula, you can add the `use-stacked: true` option beneath `multipliers:` which will take the value from the multipliers listed beneath and add it to the entity at each level. You can also instead choose to modify the entry for specific multipliers by changing their default value from `X` to `['Y', 'STACKED']`, where `Y` represents your new stacked value for that multiplier.<br />An example of this in action might be `max-health: ['5.0', 'STACKED']`, where a vanilla unlevelled zombie would have 20hp; a Level 1 would have 25hp; Level 2 at 30hp; Level 3 at 35hp, etc. 
|`creeper-max-damage-radius:`|This represents the radius of a Creeper explosion.<br />Minecraft's vanilla value is `3`, a stronger middle ground would be `5`; anything higher than `10` is basically a nuke and is not recommended unless you're into that :3 .
|`tiered-coloring:`  `LVL-LVL:`  `default:`|This represents the beginning of the Tiered Coloring system tree, where you define the settings necessary to utilize the `%tiered%` tag which can be used within the `nametag:` config option. To apply a color based on the current level of an entity.<br />You would establish a level range at `LVL-LVL:` and then either a Hex or Minecraft Color Code prefixed with an `&` in place of the `color`.<br />You can establish a `default:` color which would apply to any entity which has spawned or was summoned in a level range which is not already specified.
|`sunlight-intensity:`|This represents an additional damage amount applied to entities which burn in the sunlight.<br />This is a useful tool to help kill off higher level entities whose health can exceed the damage of the sun.
|`baby-mobs-inherit-adult-setting:`|When set to `true`, this setting will apply any condition set to an EntityType to both it's adult and baby versions if one is available.<br />When set to `false`, this will separate the EntityType into it's adult (default) and baby form, prefixed with `BABY_`.<br />**Example:** `ZOMBIE` and `BABY_ZOMBIE`. 
|`level-inheritance:`|When set to `true`, any entity which undergoes a transformation event will keep it's previous applied setting.<br />When set to `false`, the newly transformed entity will attempt to relevel itself under it's new status.<br />An example of a transformation event would be when a larger slime breaks into smaller slimes, or when a Villager transforms into a Zombie Villager and back again.
|`passenger-match-level:`|When set to `true`, any entity which spawns as a `Passenger` combination will share the same level as generated by the lowest entity in the stack (the one moving the Passenger(s) around). Whatever level that lowest entity would have generated, the passengers will match that level. When set to `false`, each entity will generate it's own level based upon it's own levelling strategy!
|`vanilla-bonus:`|By default, LevelledMobs will not alter the vanilla attribute bonus modifiers (prior to LM3.7.4, we did!). You can exclude or allow these bonuses before LevelledMobs potentially modifies these values.<br />Details taken from: [minecraft.fandom.com/wiki/Attribute](https://minecraft.fandom.com/wiki/Attribute)<br />`ATTACKING_SPEED_BOOST` - Fixed value of 6.2 for Endermen and 0.45 for Zombie Pigmen; exists only when attacking.<br />`BABY_SPEED_BOOST` - Fixed value of 0.5; exists only for baby Zombies and baby Zombie Villagers.<br />`COVERED_ARMOR_BONUS` - Fixed value of 20.0 for Shulker exists only when fully closed.<br />`DRINKING_SPEED_PENALTY` - Fixed value of -0.25 for Witches when drinking a potion.<br />`FLEEING_SPEED_BOOST` - Fixed value of 2 used by all passive mobs when fleeing.<br />`LEADER_ZOMBIE_BONUS` - Has a (small) random chance of being generated on a zombie when spawned. For Spawn Reinforcements Chance, random number between 0.5 and 0.75. For generic.max_health, random number between 1.0 and 4.0.<br />`RANDOM_SPAWN_BONUS` - Generated upon spawning; a random number from a Gaussian distribution ranging from 0.0 to 0.05.<br />`RANDOM_ZOMBIE_SPAWN_BONUS` - Generated upon spawning; a random number between 0.0 and 1.5.<br />`SPRINTING_SPEED_BONUS` - Fixed value of 0.3 used by all mobs (including players) when sprinting.<br />`ZOMBIE_REINFORCE_CALLEE` - Fixed value of -0.05 created for each zombie spawned as a reinforcement.<br />`ZOMBIE_REINFORCE_CALLER` - Fixed value of -0.05 created each time a zombie spawns another zombie as reinforcement.<br />
|`use-custom-item-drops-for-mobs:`|When set to `true`, this will enable the LM CustomDrops system.<br />When set to `false`, LM will ignore the CustomDrops entirely.
|`entity-name-override:`  `LVL-LVL:`|This config option has multiple methods to implement it. You can use the single line item method, such as `SKELETON: 'Jack'`; multiple randomly selected options, such as `SKELETON: ['Jack', 'Sally', 'Sandy Claws']`; or checking levels of the entity prior to application, as demonstrated in the code above (if specified level, then use specific custom name).<br />You can also make use of the tag `%displayname%`, which will insert the entity's name into the newly applied name. This would be useful when applying one rule to multiple EntityTypes.
|`nbt-data:`|This config option requires the soft-dependency [**NBT-API**](https://www.spigotmc.org/resources/nbt-api.7939/) to function. This allows you to apply NBT tags to entities which have spawned. This *adds* the NBT tag to whatever list of NBT tags the mob already has (nothing is reset/overridden).<br />A useful toolset for crafting even more unique styles of entities.
|`use-droptable-id:`|This config option requires the LM CustomDrops system to be enabled.<br />It allows you to select a singular drop table from the CD to apply to entities selected through LM's Rules system, allowing for highly dynamic drop conditions. Can reference multiple drop table ids.
|`lock-entity:`|When set to `true`, nametags and custom drop rules will be locked to the entity so it won't change even if a different rule gets applied to the entity later.
|`maximum-death-in-chunk-threshold:`|This controls the chunk kill count system. When a number greater than 0 is used then the system is enabled and any custom drops that are configured with `use-chunk-kill-max` will not drop once this threshold is met.
|`max-adjacent-chunks:`|The number of chunks adjacent to the chunk that an entity died in will be considered for meeting the `maximum-death-in-chunk-threshold` criteria.
|`chunk-max-cooldown-seconds:`|When a chunk kill max is reached, a timer is activated based on this setting until drops are enabled again
|`disable-vanilla-drops-on-chunk-max:`|When the chunk kill threshold is reached, this setting will determine if vanilla drops are disabled or not.
|`spawner-particles`|This applies only to LM spawners, it is the particle effect used when a mob is spawned. Can be any value from: https://hub.spigotmc.org/javadocs/spigot/org/bukkit/Particle.html
|`spawner-particles-count`|How many particles will be spawned when a mob spawns from a LM spawner.

***