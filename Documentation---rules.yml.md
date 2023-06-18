```
This page was last updated for LevelledMobs 3.10.3 b763
```

***

# Rules Configuration

LevelledMobs' `rules.yml` file allows you to craft truly modular **Custom Rules** which either modify or extend the **Default Rule** that are applied to any and all EntityTypes.
The rules file is broken into three major sections: **Presets**, **Default Rule**, and **Custom Rules**.
This documentation provides a general understanding of how the rules file works.

For more details, learn how to use the different [conditions](https://github.com/lokka30/LevelledMobs/wiki/Documentation---Conditions), [strategies](https://github.com/lokka30/LevelledMobs/wiki/Documentation---Strategies), and [apply-settings](https://github.com/lokka30/LevelledMobs/wiki/Documentation---Apply-Settings).

***

# Universal Mob Groups:
LevelledMobs includes several groups of entities which are bundled together in a convenient to recognize format. Each of these groups function as their own EntityType when using `allowed-groups:` or `excluded-groups:`, which allows you to select multiple entities at once. You can incorporate `included-list:` or `excluded-list:` to make an exception to a specific entity within the group.

You can also craft your own entity OR biome custom groupings within the rules file. These groups cannot be used inside Custom Drops at the moment, but will be accessible in the future; check back later!

|EntityType Universal Groups|Description
|:-:|:---
|`all_mobs`|All entities whether they are levelled or not.
|`all_levellable_mobs`|All entities which have been levelled.
|`all_hostile_mobs`|All hostile entities, whether they are levelled or not.
|`all_passive_mobs`|All passive entities, whether they are levelled or not.
|`all_overworld_mobs`|All Overworld entities, whether they are levelled or not.
|`all_nether_mobs`|All Nether entities, whether they are levelled or not.
|`all_flying_mobs`|All flying entities, whether they are levelled or not.
|`all_ground_mobs`|All ground-limited entities, whether they are levelled or not.
|`all_aquatic_mobs`|All aquatic entities, whether they are levelled or not.

***

# Presets:
LM allows you to craft certain sets of config options into sets known as **Presets**, which can be applied within either the **Default Rule** or any **Custom Rules** utilizing the `use-preset:` config line. For example:

```yml
custom-rules:
  - enabled: true
    name: 'Custom Rule'
    use-preset: presetName, otherPresetName
    use-preset:
      - presetName
      - otherPresetName
```

```yml
presets:
  presetName:
    name: 'Preset Name'
    system:
```

The **Presets** section covers the first third of the file, and by default it is used to mostly populate the **Default Rule** with multiple different out-of-the-box solutions to common questions! You can edit or add your own presets to the list, or choose to not use the preset system at all. This is meant to be an aid in preventing duplicate text across the rules file.

When crafting a preset, the above structure should be followed. Beginning with the `presets:` tag, you indent two spaces and then give your preset a name to reference later, replacing `presetName:` with this value. Make sure to only use alphanumeric values, without spaces, for this value.
On the next time, two further spaces indented, you should give your preset an easy-to-read `name:`. While this is not required, you will thank yourself later!
Finally, `system:` represents either `conditions:`, `strategies:`, and `apply-settings:` depending on the type of preset you intend to build!



# Default Rule:
LM requires this section to be populated with the following minimal information in order to work with a minimum of functionality. By default, LM uses the **Presets** system explained above to populate the Default Rule with the necessary values, plus several more, in order to make things quick and easy to switch between preconfigured settings.

```yml
default-rule:
  conditions:
    worlds:
      allowed-list: ['*']
    strategy:
      random: true
    apply-settings:
      minLevel: 1
      maxLevel: 25
      multipliers:
        max-health: 5.0
        movement-speed: 0.15
        attack-damage: 2.25
        ranged-attack-damage: 2.0
        creeper-blast-damage: 1.0
        item-drop: 3
        xp-drop: 5
      nametag: '&8&l༺ %tiered%Lvl %mob-lvl%&8 | &f%displayname%&8 | &f%entity-health-rounded% %tiered%%heart_symbol% &r%health-indicator% &8&l༻'
      creature-death-nametag: '%tiered%Lvl %mob-lvl%&8 | &f%entity-name%'
```



# Custom Rules:
LM comes out-of-the-box with several different **Custom Rules** which are both enabled and disabled.
These are used to both achieve specific results, such as disabling the levelling of passive entities with the first custom rule, as well as provide multiple examples of how to use custom rules in unique ways.

## Priority:
By default, LM processes the rules in a linear order: from top to bottom; from the Default Rule to the first through last Custom Rule. You can establish a priority config line within a custom rule which will override it's position in the queue, allowing it to process earlier or later than the rest of the stack. Remember that the Default Rule will **ALWAYS** process first before any Custom Rules to populate any necessary default values.
Below represents an example of how priority alters the 'stack queue' of Custom Rules:

```yml
custom-rules:
  - enabled: true
    name: 'Run before the stack, as the highest priority, as the first rule processed after the Default Rule'
    priority: 2

  - enabled: true
    name: 'Run before the stack, after any higher priority'
    priority: 1

  - enabled: true
    name: 'Run the queued stack (same as not listing priority)'
    priority: 0

  - enabled: true
    name: 'Run the queued stack (same as priority: 0)'

  - enabled: true
    name: 'Run after the stack, before any lower priority'
    priority: -1

  - enabled: true
    name: 'Run after the stack, as the lowest priority, at the very end'
    priority: -2
```

Below represents the basic framework of a Custom Rule:

```yml
custom-rules:
  - enabled: true
    priority: 1
    name: ''
    use-preset: 
    conditions:
    strategies:
    apply-settings:
```

* `- enabled:` - This represents whether the custom rule is enabled or disabled.
* `priority:` - This value overrides the custom rule's processing order.
* `name:` - This represents an easy-to-read representation of the Custom Rule for debug purposes.
* `use-preset:` - This allows you to use a Preset within a Custom Rule.
* `conditions:`, `strategies:`, and `apply-settings:` - [These are elaborated on further here](#).

Any detail not specifically listed within the custom rule will gather that information from the Default Rule when constructing the final custom rule to apply to an entity. For example:

```yml
default-rule:
  conditions:
    worlds:
      allowed-list: ['*']
    entities:
      allowed-list: ['all_mobs']

custom-rules:
  - enabled: true
    name: 'Disable Passive Entities'
    conditions:
      entities:
        allowed-list: ['all_passive_mobs']
    apply-settings:
      maxLevel: 0
```

The way the above structure is read, starting from the default rule: All worlds are levellable, and all entities are levellable based on the Default Rule. When the custom rule was crafted, I did not need to specify what world the rule would apply to, since it grabs the value 'all worlds' from the Default Rule. I do however, have to specify the entities, because if I didn't the custom rule would apply to 'all entities' as stated in the Default Rule. Finally, I have applied the level `0` which disables levelling to the passive entities in all worlds.

*** 

> Note: Some config options utilize a custom `MODALLIST` to configure it.  
> Below demonstrates how to use the MODALLIST feature:

```yml
  allowed-list: ['']
  allowed-groups: ['']
  excluded-list: ['']
  excluded-groups: ['']
  merge: true
```

The `MODALLIST` config option is fairly simple to read, as they're used exclusively within the Conditions section.
If a config option requires a `MODALLIST` to be used, such as `entities:` and `worlds:`, then what config option you use will depend on your needs.

**Example:** If you want the Condition to check whether an entity is a zombie, you would use the `allowed-list:`, meaning the list will only allow those which you have approved to meet the Condition.

**Example:** If you want the Condition to apply to all entities, except for the zombie, then you would use `excluded-list:`, meaning the list will use all entities except for those you excluded from meeting the Condition.

**Example:** If you want the Condition to apply to the `all_passive_mobs` group, but want to skip the chicken, you would use a combination of `allowed-groups:` and `excluded-list:`, where you would allow all passive entities in the group to meet the Condition, while your `excluded-list:` would be removed before final processing.

Some `MODALLIST` config options cannot utilize the '-groups' line, as those are limited to Entity and Biome custom or universal groups. If you wish to combine the lists of two different `MODALLIST` from the Default-Rule and a Custom Rule, then simply add a `merge: true` line to the end of the config list to combine the two together.