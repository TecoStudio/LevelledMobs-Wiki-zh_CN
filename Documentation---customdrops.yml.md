```
This page was last updated for LevelledMobs 3.8.2 b721
```

***

# Custom Drops Configuration

LevelledMobs' `customdrops.yml` file allows you to build custom drops utilizing many different config options to create unique materials and custom commands to add to or replace an entity's drops.

[View Latest Default File](https://github.com/ArcanePlugins/LevelledMobs/blob/master/src/main/resources/customdrops.yml)

**Need a sample config file to help you get a bearing?**
UltimaOath is currently working on a `customdrops.yml` file which will contain thousands of lines of potential Custom Drops to use within your server. The file is being maintained and is always being changed and updated. Once it is finished, a final copy will be left here. In the meantime, [you can keep up with the progress here](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/exampleconfigs/customdrops.yml)!

***

# Defaults:
These config options will apply to all drops constructed within CustomDrops _unless_ you have modified a drops' individual properties to override these default settings. Each of these must have a value in order for LM's CD to function properly, but once it is set here, you do not need to set it within your individual drops if the value would not change. These defaults apply to all systems within the CD file, including **Drop Tables**.

> ### For any value listed as a _percent_: `1.0` = 100% ; `0.0` = 0%

```yml
defaults:
  chance: 0.2
  use-chunk-kill-max: true
  amount: 1
  minLevel: -1
  maxLevel: -1
  damage: 0
  custommodeldata: -1
  min-player-level: -1
  max-player-level: -1
  nomultiplier: true
  nospawner: false
  equipped: 1.0
  equip-offhand: true
  override: false
  maxdropgroup: 1
  priority: 0
  player-caused: true
  item_flags: ''
  groupid: ''
  overall_chance: 0.0
  nbt-data: ''
  only-drop-if-equipped: false
  player-level-variable: ''
  name: ''
  lore:
    - ''
    - ''
  enchantments:
    ENCHANTMENT: X
  enchantments:
    ENCHANTMENT:
      shuffle: false
      default: 1
      X: 0.5
  overall_permission: ['']
  permission: ['']
  cause-of-death: ['']
  run-on-spawn: false
  run-on-death: true
  delay: 0
```

|Config Line Option|Description
|:-:|:---
|`chance:`|This represents the percent chance of an individual CD being dropped.
|`use-chunk-kill-max:`|If the chunk kill count system is enabled in rules.yml, then setting this to true will cause the custom drop to not drop once the threshold has been met, until the cooldown time expires.
|`amount:`|This represents the number of individual CD being dropped. This may be ranged, such as `1-3`, where a value is randomly selected from between the two min/max values.
|`minLevel:`  `maxLevel:`|This represents the minimum and maximum level required of the entity before an individual CD will drop.<br />Replace with `-1` to disable the particular level check.
|`damage:`|The amount of damage the item will have. Can use a number or a number range. The higher the value, the more damaged it will be.
|`custommodeldata:`|This is an advanced config option; This represents a custom model to apply to the material CD.
|`nomultiplier:`|This represents the check whether a CD will or will not multiply according to the `item-drop:` value of the killed entity.
|`nospawner:`|This represents the check whether a CD will or will not apply to an entity spawned by a Spawner Cube.
|`equipped:`|This represents the percent chance of an individual CD being equipped by the entity if it is able to.<br />It will first attempt to place in the hands, then the skull, and otherwise will ignore if the entity could not normally equip an item (such as Silverfish).
|`equip-offhand:`|If `equipped:` was successful, and this setting is `true`, then it will equip the item to the off-hand rather than primary if it is unoccupied.
|`name:`|This represents the name to apply to the material drop when it is used on a `MATERIAL` or `PLAYER_HEAD` drop.<br />When used for a `customCommand`, it is merely a debug value.<br />You can use Minecraft's color code or if your server software supports it, HEX colors!
|`lore:`|This structure of config options allows you to set multiple lines of lore to apply to a `MATERIAL` or `PLAYER_HEAD` drop.<br />You can use Minecraft's color code or if your server software supports it, HEX colors!
|`enchantments:`<br />`ENCHANTMENT:`  `X`<br />`ENCHANTMENT:`  `X: 0.5`<br />`shuffle:`  `default:`|This structure of config options allows you to apply enchantments to items.<br />Replace `ENCHANTMENT:` with the name of the enchantment, and replace `X` with the strength of that enchantment.<br />For example, `UNBREAKING: 2`.<br />You can also specify the chance of a specified enchantment level being applied to an item, by using `X: 0.5` beneath the `ENCHANTMENT:`; the `X` represents the strength of the enchantment, while the `0.5` represents the chance of that enchantment level being applied.<br />Within this section you can specify `shuffle: false`, which will process the enchantment level chances to apply in order rather than at random. The setting `default: X` will use the specified level if none of the enchantment level chances succeed.
|`override:`|This will determine whether LM will process CD alongside the vanilla drops, or replace them entirely.
|`maxdropgroup:`  `groupid:`|Using `groupid:` within multiple material items under the same `EntityType` or `drop-table:` will combine these CD into their own separately processed group. When combined which `maxdropgroup:`, which limits the number of drops within the same group can be dropped, and the various `chance:` config options, helps to chain tiers of drops together.
|`priority:`|By default, CD processes the drops in a similar fashion to how LM processes the rules tree.<br />By setting a `priority:` on an individual CD, you are letting certain items process first before others.
|`player-caused:`|This represents the check on whether the entity's death was caused by a player, or whether it was environmental.<br />It is recommended that you do not change this from `true`, as making this `false` will cause any levelled entity who dies to potentially drop your special customized drops.
|`overall_chance:`|This represents a percent chance of any of the EntityType's CD being processed at all. This only needs to be placed once for an EntityType, and if the chance fails, none of the CD for that EntityType will process.
|`nbt-data:`|This allows you to specify any NBT data to apply to a material drop.<br />**NOTE:** This requires the soft-dependency **[NBT-API](https://www.spigotmc.org/resources/nbt-api.7939/)**
|`item_flags:`|This allows you to specify the various `ITEM_FLAGS` that Minecraft provides to apply to materials.<br />`HIDE_ATTRIBUTES` - Will hide attributes, like damage.<br />`HIDE_DESTROYS` - Will hide what the Item can destroy.<br />`HIDE_DYES` - Will hide the dye color applied to Item.<br />`HIDE_ENCHANTS` - Will hide enchantments on Item.<br />`HIDE_PLACED_ON` - Will hide where the Item can be placed.<br />`HIDE_POTION_EFFECTS` - Will hide potion effects placed on the Item.<br />`HIDE_UNBREAKABLE` - Will hide unbreakable status of Item.
|`only-drop-if-equipped:`|This represents a check, if an Entity has `equipped:` the item successfully, whether the `chance:` to drop will apply. If set to `true`, then only if the item was successfully equipped will the `chance:` be attempted in the drop. If set to `false`, then the item will attempt to drop regardless of it's equipped status.
|`overall_permission:` `permission:`|A `MODALLIST` config option; this represents a check against the nearest player to the entity, OR the player who killed an entity, depending on it's implementation. All permissions as registered as `levelledmobs.permission.<node>`, where `<node>` represents the value of this config. For example, if your permission was `levelledmobs.permission.vip`, you would configure it as such: `permission: ['vip']`. Using `overall_permission:` will apply to all items within the set, while `permission:` applies to each singular item.
|`cause-of-death:`|A `MODALLIST` config option; this represents a check against how the entity was killed. This only takes into account the final blow, and will ignore `player-caused: true`, since the cause of death will not typically involve player interaction ('fire' dealing the damage, versus the player).
|`min-player-level:` `max-player-level:`|This represents the minimum and maximum Minecraft level required of the Player before an individual CD will drop.<br />Replace with `-1` to disable this particular level check.
|`player-level-variable`|If this config option is set, the above `min-player-level:` and `max-player-level:` will reference this variable instead of the player's Minecraft level. You can use any `PAPI` placeholder tag in this place similar to how the `Player Levelling` strategy uses the variable to generate levels.
|`external-amount`|When used with LM_Items, this sets the amount internally to the specified plugin
|`type`|When used with LM_Items, this sets the item type (currently only supported with MMOItems
|`run-on-spawn`|Applicable only to custom commands, determines if it will be executed when a mob spawns in
|`run-on-death`|Applicable only to custom commands, determines if it will be executed when a mob dies
|`delay`|Applicable only to custom commands, this is the number of ticks that will elapse before the command is executed

# Further Drop and Command Attributes
While both material and command drops can utilize any of the Default config options listed above, there are two instances where special config options are available.

There are several placeholders available which you can use when combined with a `customCommand:` drop to fill in certain necessary dynamic inputs within a command.

|Config Line Option|Description
|:-:|:---
|`%mob-lvl%`|This represents the killed entity's level.
|`%player%`|This represents the player who killed the entity.
|`%displayname%`|This represents the killed entity's CustomName field.
|`%entity-name%`|This represents the killed entity's EntityType.
|`%entity-max-health%`|This represents the killed entity's maximum health, exactly.
|`%entity-max-health-rounded%`|This represents the killed entity's maximum health, rounded to nearest whole number.
|`%wg_region%`|This represents the WorldGuard region where the entity died.
|`%world%`|This represents the world name where the entity died.
|`%X%` `%Y%` `%Z%`|This represents the three coordinate points for the location of the entity's death.



```yml
- PLAYER_HEAD:
    mobhead-id: ''
    mobhead-texture: ''
- MATERIAL:
- ENCHANTED_BOOK:
    enchantments:
      ENCHANTMENT: X
- customCommand:
    command: ''
    command: ['', '']
    ranged_A: ''
    ranged_B: ''
    name: ''
```

You can specify a PLAYER_HEAD block drop with it's own texture, using the UUID under mobhead-id AND the TEXTURE value under mobhead-texture:. You can search online for 'minecraft player head database' to find appropriate values. While specifying both is good practice for redundancy, you are only required to specify one or the other to utilize the feature.

MATERIAL drops gather their config options from the Defaults section listed above. Any config option listed there can be used within any MATERIAL, PLAYER_HEAD, or customCommand drop. 'customCommand:' tells CD that you wish to setup a command to process like a drop for an EntityType. In order for this feature to function, it requires at minimum the 'command:' config option with a valid console formatted command present. You can also use multiple commands at once by listing them as demonstrated above.
An example of a valid command might be 'effect give %player% strength %ranged_a% %ranged_b%'.

ENCHANTED_BOOK is a special type of MATERIAL drop which will enable anvil-ready enchanted books by utilizing the `enchantments:` config option.

The tags prefixed with `ranged_` are unique. These allow you to construct a random number generator to be used within commands as placeholders. The example config above demonstrates how you would utilize the ranged config option, appending an A/B/C/D, et cetera to the end of `ranged_` creates the tag, while the value represents a range of potential values which could be applied to the placeholder tag present in the individual command drop.
Using the previous example command, with the `ranged_A: 1-2` and `ranged_B: 3-5`, then the first tag would be any value between 1-2, while the second would be any value between 3-5 when utilized within the command being activated.



# Universal Groups:
LM includes several groups of entities which are bundled together in a convenient format. Each of these groups function as their own EntityType, applying to multiple entities at once.
You can refer to the [EntityType Universal Groups](https://github.com/lokka30/LevelledMobs/wiki/Documentation---rules.yml#universal-mob-and-biome-groups) for the different types!



# EntityTypes:
LM has listed all vanilla entities as of Minecraft 1.17 within the CD file. You should locate the entity you wish to modify instead of adding additional entities at other spots within the config, as they will most likely not process as expected. You may delete any entities you do not use if you so choose, as you can always add them back again later.



# Drop Tables
CD includes the Drop Table system, which allows you to construct groups of materials or custom commands which can be attached to any EntityType as a single line item utilizing `usedroptable: tableName`, helping to reduce any instances of duplicate drops covering multiple entities. This can also be used to craft 'tiered' drops.

```yml
PUT_ENTITY_TYPE_HERE:
  - usedroptable: 'putTableNameHere'
```

When constructing drops with the Drop Table, you can replicate the same formatting used for any other drop, replacing the EntityType with the tableName.

> **Remember:** Any configuration option not specified in the Drop Tables will collect those values from your Defaults.

# External Plugin Support
If you want to use custom items from external plugins, take a look at LM Items. <br>
This plugin bridges the gap so you can use third party items natively. <br>
Download from https://www.spigotmc.org/resources/lm-items.102081/