```
This page was last updated for LevelledMobs 3.9.3 b735
```

***

# Understanding the default `rules.yml` configuration file

LevelledMobs' `rules.yml` file allows you to craft truly modular **Custom Rules** which either modify or extend the **Default Rule** that are applied to any and all EntityTypes.
The rules file is broken into three major sections: **Presets**, **Default Rule**, and **Custom Rules**; though the main features come from _establishing the default rule_ by which all entities under the established default conditions will be levelled, then by _adding exceptions to the default rule in the form of custom rules_, where you can establish a set of conditions which would apply changes to the default rule under those conditions. We created the presets section so that any frequently referenced conditions or settings can be quickly added to either the default or custom rule(s) to help reduce the size of the file, though you do not have to reference or include the preset section at all so long as you have manually written in your conditions and settings.


***


# The Default Rule
The `default-rule:` of the `rules.yml` file establishes the rules under which most entities will or will not be levelled. This provides LevelledMobs a baseline from which to work when setting entity stats and levels. Under the default configuration, we make liberal use of the `presets:` section to establish most of the default `conditions:`. Those presets include `allowed_worlds`, `weighted_random_Levelling`, `average_challenge`, and `nametag_using_numbers`. If you reference the `presets:` of the same name, you will see that those presets include various `conditions:`, `strategies:`, and `apply-settings:`. Since they're referenced in the `default-rule:`, each of those `presets:` are essentially copied into the `default-rule:`. If the same configuration option is set under the same default rule, then only the last one listed will be listened to. 

For the `default-rule:`, the bare-minimum you need to tell LevelledMobs would be: what world(s) do you want LevelledMobs to apply in, what strategy you want to use to level the entities, and how strong you want those entities to be. Secondary settings include things like applying a nametag to the entity to display its altered stats and figures, or setting a condition restricting entities from Spawner Cubes from receiving a level.

Generally speaking, you want your `default-rule:` to be as open as you would desire for your server. This section is meant to limit from the beginning the changes that LevelledMobs makes, from removing it entirely from a specific world to establishing the core-strategy to use overall. Don't worry, any changes you need to make can be made via a custom rule.


***


# The Custom Rules
The `custom-rules:` of the `rules.yml` file establishes any exceptions to the default rule. Under the default configuration, we use four distinct custom rules which provide player-tested exceptions which we find benefit the overall experience. Each of these rules can be changed, or removed entirely based on your servers' needs.

***

> CR - NoLevel All Passive + EntityTypes
```yaml
  - enabled: true
    name: 'CR - NoLevel All Passive + EntityTypes'
    use-preset: allowed_worlds
    conditions:
      entities:
        allowed-groups: [ 'all_passive_mobs' ]
        allowed-list: [ 'BABY_', 'ENDER_DRAGON', 'WITHER', 'VILLAGER', 'ZOMBIE_VILLAGER', 'WANDERING_TRADER', 'PHANTOM', 'BAT', 'RAVAGER', 'WARDEN' ]
    apply-settings:
      maxLevel: 0
```
By default, all entities in the selected `default-rule:` world(s) will receive a level.
This first custom rule sets a condition check for: all entities within the 'Passive' group, which Minecraft considers entities like chickens, pigs, sheep, etc. , a handful of individual entities (`'ENDER_DRAGON', 'WITHER', 'VILLAGER', 'ZOMBIE_VILLAGER', 'WANDERING_TRADER', 'PHANTOM', 'BAT', 'RAVAGER', 'WARDEN'`), and all `BABY_` entities (which represent all baby entities).
Then we tell LevelledMobs that if any of those entities appear, we set the `maxLevel: 0`. When an entity is level 0, it is considered unlevelled by LevelledMobs and will not be affected by any changes.
These entities have been selected for various reasons, some obvious some less so. Having only hostile entities levelled made sense to us, and we removed the levelling from entities like the Villager, Zombie Villager, Wandering Trader to protect their abilities. Then there are quality of life additions like the Bat which is considered a 'Neutral' mob. Finally, we've also included the mini-bosses the Wither and Warden, as well as the 'final boss' the Ender Dragon, to let you the user decide how to let these entities loose.

***

> CR - Custom Nether Levelling
```yaml
  - enabled: true
    name: 'CR - Custom Nether Levelling'
    conditions:
      worlds: 'world_nether'
    strategies:
      y-coordinate:
        start: 100
        end: 40
        period: 0
```
By default, any world that is selected in the `default-rule:` will use the strategy established there to apply levels. While this is perfectly acceptable, we considered that since the Nether world is more a vertical map it would make sense to change the strategy from `weighted-random` to `y-coordinate`. With this change, all entities within the Nether will follow the `default-rule:`, with this one exception altering the strategy to be applied.

***

> CR - Custom Entity Attributes
```yaml
  - enabled: true
    name: 'CR - Custom Entity Attributes'
    use-preset: allowed_worlds
    apply-settings:
      multipliers:
        custom-mob-level:
          ENDERMAN:
            max-health: 0.0
            movement-speed: 0.0
          SILVERFISH:
            max-health: 0.0
            movement-speed: 0.0
          CREEPER:
            movement-speed: 0.025
          WITHER_SKELETON:
            max-health: 1.0
```
By default, any entity levelled under the `default-rule:` will use the multipliers established there to determine the degree to which stats are altered . We have learned over several years that some exceptions to these stats should be made for the average server. Each of these can be changed, or removed entirely, based on your needs.
This custom rule uses a sub-section of the `multipliers:` `apply-settings:` called `custom-mob-level:`, which allows you to establish changes to the default multipliers (established in the default `average_challenge`) for specific entities.

The first entity we modify is the Enderman, where we establish that the `max-health:` and `movement-speed:` of Endermen are not to be changed when if they receive a level. The purpose for this is that in a vanilla environment, when you hit an Enderman they typically gain a lot of movement speed and a teleport ability. Having a fully levelled Enderman makes this effect exponentially more deadly, as the increase in health and speed makes them nearly impossible to kill effectively. This also helps to prevent player Enderman farms from breaking.
The second entity being the Silverfish, which has the `max-health:` and `movement-speed:` changes eliminated as well for similar reasons.
The third entity being the Creeper, which has a reduced cap set on the `movement-speed:`. Creepers can be challenging, especially when levelled. This reduced movement speed keeps Creepers from charging the player and preventing them from having an honest chance to escape before they explode.
The fourth entity being the Wither Skeleton, whose Wither ability makes them challenging even under the vanilla rules. This adjusted `max-health:` helps reduce the overall challenge for these entities, while maintaining their increased attack damage and movement speed amongst other `multipliers:`.

***

> CR - Custom Zombie Piglin Levelling
```yaml
  - enabled: true
    name: 'CR - Custom Zombie Piglin Levelling'
    conditions:
      worlds: 'world_nether'
      entities: 'ZOMBIFIED_PIGLIN'
    strategies:
      random: true
    apply-settings:
      minLevel: 1
      maxLevel: 5
      multipliers:
        max-health: 1.0
        movement-speed: 0.25
        attack-damage: 0.5
        ranged-attack-damage: 0.0
        item-drop: 0.5
        xp-drop: 1.0
      tiered-coloring:
        1-5: '&#22E76B' #Green
```
By default, without this rule in place, Zombified Piglins would level like any other hostile entity within the Nether up to this point. Zombified Piglins are one of the few entities that team up when attacked, and specifically these entities form a type of hoard which chase after players for extended periods of time. We find that if we let Zombified Piglins level to their full potential under the `default-rule:`, they would become an insurmountable challenge and make the Nether generally difficult to traverse. 
Under this custom rule, we have set a condition check for any `ZOMBIFIED_PIGLIN` within the Nether. These entities would then take their `default-rule:` multipliers and replace those values with the ones established in this custom rule; all of which are lower than the default adjustments. We also provided a unique `tiered-coloring:` that adjusts the `%tiered%` output in the nametag; a purely cosmetic change.
