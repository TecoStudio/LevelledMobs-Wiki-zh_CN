```
This page was last updated for LevelledMobs 3.9.2 b734

Note that any approximated line numbers may become outdated as we update the configuration files.
```

***

## I have no idea how to get started!?

<details>
<summary>See answer</summary>

Do not worry! We know that LevelledMobs can at first glance be daunting to take on. The wiki is highly detailed, and the files are populated with many presets and examples in order to help demonstrate how to use the system. But if even that is too much, start here:


***

**Have you successfully installed LevelledMobs, and is it running on your server without error?**

Oftentimes a first and regularly overlooked step is to ensure that when you started your server that LevelledMobs encountered no issues during that process. Some plugins and server environments, while rare, will simply not work with LevelledMobs and you would be shown large walls of text in your console screaming about a particular issue. Sometimes that only happens once at the first attempted start, sometimes it's obvious and it spams your console with repeated instance after instance. If this is the case, it is best to test this plugin in a testing environment where you can isolate which plugin or issue is causing the breakdown. 
If you have already begun editing your configuration files, and you have made a mistake in the formatting of the file, then LevelledMobs will report the issue when it attempts to load those files during startup or any subsequent reload of the plugin. If LevelledMobs cannot read a file in it's entirety, then it cannot function properly, and will likely result in a broken experience. YAML is the language used for most plugins, and it is very unforgiving of mistakes; even those as simple as a missing or extra space. We recommend running your file through a free online YAML-Checker which will help identify any issues in your file.


***

**No errors? Great! Now: Understanding the Rules file.**

If you have just installed the plugin and have no errors in the console during startup or while running, then LevelledMobs should be ready to go out-of-the-box.
There is a general description of each system provided [here](https://github.com/ArcanePlugins/LevelledMobs/wiki/Understanding-the-Default-Config), but a more detailed description can be found below.
To understand how the Rules file works, I will explain how the default settings are set and selected. Firstly, the Rules file is broken into three distinct sections: `presets:`, `default-rule:`, and `custom-rules:`. The `presets:` section includes a wide variety of different systems separated into presets given their own names. For example, the presets that are used in a default configuration are named `allowed_worlds`, `weighted_random_Levelling`, `average_challenge`, and `nametag_using_numbers`. You'll notice many others which are preconfigured and ready to use should you want to switch between them. 

Below the `presets:` section sits the `default-rule:`. Here is where you tell LevelledMobs the core set of levelled entities and the conditions under which they will level. As I said a moment before, in the default configuration we use the `presets:` called `allowed_worlds`, `weighted_random_Levelling`, `average_challenge`, and `nametag_using_numbers`. You can see that those are enabled alongside a list of other disabled presets:

```yaml
default-rule:
  use-preset:
    - allowed_worlds
    - nametag_using_numbers
    #- nametag_using_indicator
    #- basic_challenge
    - average_challenge
    #- advanced_challenge
    #- extreme_challenge
    - weighted_random_Levelling
    #- spawn_Levelling
    #- lvl-mod_spawn-blended
    #- ycoord_Levelling
    #- random_Levelling
    #- lvl-mod_player-variable
    #- lvl-mod_apply-variance
```

The first preset, `allowed_worlds`, sets the conditions for what worlds that LevelledMobs will apply. If you refer to the preset of the same name, you can see that we allow LevelledMobs in 'all worlds except for `world_the_end`'. 

```yaml
  allowed_worlds:
    # This controls the allowed worlds to apply levels too.
    name: 'Excluded Worldlist'
    conditions:
      worlds:
        # allowed-list: ['*']
        excluded-list: [ 'world_the_end' ]
```

The second preset, `nametag_using_numbers`, controls a majority of the nametag related settings. This system has a similar preset called `nametag_using_indicators` which functions essentially the same, but uses a secondary system to add distinction to the ability. Either way, you can choose to edit it to your liking.

```yaml
  nametag_using_numbers:
    #   This controls the nametag, where the health is displayed using %entity-health-rounded%
    name: 'Nametag - Health Numerical'
    apply-settings:
      nametag: '&8&l༺ %tiered%Lvl %mob-lvl%&8 | &f%displayname%&8 | &f%entity-health-rounded%&8/&f%entity-max-health-rounded% %tiered%%heart_symbol% &8&l༻'
```

The third preset, `average_challenge`, refers to one of four playtested `_challenge` options which you can easily switch between, or choose to edit the default, or create one that is entirely your own (we recommend copy/pasting another `_challenge` preset and changing the name of the preset to something unique like `epic_challenge`). The `average_challenge` was tested on a vanilla Minecraft server under Normal difficulty, and meant to produce entities that feel like the vanilla Hard difficulty; the `basic_challenge` is an easier version, while `advanced_challenge` and `extreme_challenge` are meant to test even the toughest of players in full enchanted vanilla armors.

None of these take into account any customization added to your own server with regards to player abilities (things like McMMO, AureliumSkills, etc. which boost a players damage output or health, or provides non-vanilla enchantments or abilities), so you will want to take that into account when adjusting the difficulty.

Each of the `_challenge` presets are arranged the same: establishing the `maxLevel:`, establishing the `multipliers:`, and then giving details for other systems like `tiered-coloring:` which adjusts the `%tiered%` placeholder within the `nametag_using_numbers` or `nametag_using_indicators`, or the `health-indicator:` settings regarding the number of 'indicators' and their value in health points. There are two means of adjusting the difficulty: if you want to keep the actual challenge the same, but want to change the difference between the levels to be easier or harder, you would simply adjust the `maxLevel:` without adjusting the `multipliers:`; this would spread or shrink the multiplier over a different level range, from one to the current `maxLevel:`. If you want to adjust the actual difficulty of the entities, you need only adjust the `multipliers:` first to determine how difficult your entities will be; once you are satisfied, then you can adjust the `maxLevel:` to spread or shrink that difference over the level range. 

As of `LM 3.9`, you can use the original arrangement for multipliers, which sets the 'percent increase at max level' for the multiplier (for example, `max-health: 5.0` would be a 500% increase when at max level); or you can choose to use the `STACKED` option, which simply adds a value to each multiplier at each level increase (for example, `max-health: ['5.0', 'STACKED']` would mean at each level starting with Level 1 to the `maxLevel:`, `5.0` will be added to the health of the entity). 

With `tiered-coloring:`, you can set the color of the `%tiered%` placeholder used in the nametag systems. Refer to the [wiki](https://github.com/ArcanePlugins/LevelledMobs/wiki/Documentation---Apply-Settings) for how to use this system.

```yaml
  average_challenge:
    name: 'Average-Challenge Multipliers'
    apply-settings:
      minLevel: 1
      maxLevel: 25
      multipliers:
        max-health: 5.0
        movement-speed: 0.15
        attack-damage: 2.25
        ranged-attack-damage: 2.25
        creeper-blast-damage: 0.75
        item-drop: 3.0
        xp-drop: 5.0
        #       Special Multipliers (0.0 Min - 1.0 Max)
        armor-bonus: 0.2
        armor-toughness: 0.15
        ##   optional: use the stacked multiplier instead
        # max-health: [ '4.25', 'STACKED' ]

      tiered-coloring:
        1-5: '&#22E76B' #Green
        6-10: '&#528CFF' #Blue
        11-15: '&#FFCD56' #Yellow
        16-20: '&#F2003D' #Red
        21-25: '&#B447FF' #Purple
        default: '&#FFFFFF' #White
      health-indicator:
        scale: 4
        max: 5
        merge: true
```

At this point we have told LevelledMobs where it can level entities, and the we told it what the level range was and how difficult the entities will be. Now we need to tell it how to assign these levels to the entities. With the fourth preset called `weighted_random_Levelling`, we tell LevelledMobs that it should select a level to apply to entities by making the highest level the least likely, and the lowest level the most likely. The other options and how to use them are detailed further in the [wiki](https://github.com/ArcanePlugins/LevelledMobs/wiki/Documentation---Strategies). 

```yaml
  weighted_random_Levelling:
    # This Strategy Preset controls Weighted Random Bias.
    name: 'LVLling Strategy - Weighted Random'
    strategies:
      weighted-random: true
```

You can choose to edit the presets of the same name above to make changes to the default rule of your worlds (for example, instead of changing to `advanced_challenge` to get a world with entities from 1-50 levels, you can simply edit the `maxLevel:` value under the `average_challenge` preset from the default of 25 to 50).

You can create your own presets with unique names to be used elsewhere (for example, you could craft a similar preset to `average_challenge` called `epic_challenge` and give it unique values).

You can disable one preset and exchange it for another preset of the same type (for example, you could disable `weighted_random_Levelling` and replace it with `spawn_Levelling` to use the spawn distance to determine levels).

There are also special presets which start with `lvl-mod_` which represent various addon systems that adjust the level of an entity AFTER it has been assigned by a Levelling strategy. For example, `lvl-mod_player-variable` refers to a system which adjusts the level of an entity based on a variable produced by the nearest player; `lvl-mod_apply-variance` adds a random plus or minus to a level; `lvl-mod_spawn-blended` adds a height metric to the `spawn_Levelling` preset should it also be enabled.


***

**Wow that's a huge text wall!**

And that was just describing much of the Presets section! But don't worry, if you've made it this far, you're more than 85% of the way to the finish line! All that remains are the various conditions and settings which did not necessarily fit within a preset under the `default-rule:`, all of which are described in detail in their respective wiki sections for Conditions, Strategies, and Apply-Settings. While you do not have to use the `presets:`; you could simply include all of the pertinent conditions and levelling strategies line by line in the `default-rule:`; we find that using the presets make things significantly easier to manage; especially if you intend to further customize the plugin within the Custom Rules.


***

**Custom Rules - There's a rule for that!**

This section consists of exceptions or adjustments to the `default-rule:`. If you took our original default config and removed all of the custom rules, the plugin would still function but would have no exceptions to levelling for passive entities (or a handful of other individual ones like villagers, wandering traders, or all 'baby' entities), would not provide a custom levelling strategy for the Nether world which uses the height of the world rather than the `default-rule:` of a weighted random, would not provide entity-specific adjustments like removing the `movement-speed:` and `max-health:` `multiplier:` from endermen to protect player farms and from a swarm of endermen moving too fast (amongst other edits), and finally zombie pigmen would not be nerfed in order to protect players from an unfair swarm. Each of these custom rules are playtested and believed to be in the best interest of your server; but we obviously do not know every situation and leave the choices up to you!

From here you can continue adding Custom Rules by establishing a set of conditions which you want to check for, and then establishing any settings or strategies it would have under those conditions. The wiki is full of possible [conditions](https://github.com/ArcanePlugins/LevelledMobs/wiki/Documentation---Conditions) to choose from.


***

**The End is Near: Custom Drops**

You've finally made it to the end: our Custom Drops system allows you to set a wide variety of vanilla items alongside many 3rd party plugin items which are synced to our optional `LM_ITEMS` [plugin](https://www.spigotmc.org/resources/lm-items.102081/). You can also use the `NBT-API` [plugin](https://www.spigotmc.org/resources/nbt-api.7939/) to craft custom items internally by directly setting NBT data on the item. 

There is far too much to explain in detail here, especially when there is an entire section of the wiki dedicated to it. But for those wanting a solid library of examples, look no further than the [Sample Custom Drops page](https://github.com/ArcanePlugins/LevelledMobs/wiki/Sample-CustomDrops), which includes over three thousand lines of custom drops which are free to copy and modify to suite your needs. This helps to demonstrate the power and ability of these systems (the sample files use the Drop Table system within Custom Drops; it is recommended to implement these tables [via the following method](https://github.com/ArcanePlugins/LevelledMobs/wiki/Sample-Custom-Rules#using-drop-tables-with-custom-rules), as it gives you the combined strength of the Custom Drops modifiers/conditions, and the Custom Rules conditions).


***

**Did you say 'Speak to a Human'?**

After everything you're still confused or have a question? Don't hesitate to come to the [Arcane Plugins discord](https://www.discord.io/arcaneplugins). Follow the rules/readme there and you will find quick and efficient support who will, when they're available, respond to each and every question or concern! 


***

</details>


## How do I enable/disable LevelledMobs in certain worlds?

<details>
<summary>See answer</summary>

Around line 180 in `rules.yml`, you should see the `allowed_worlds` preset:
```yaml
 allowed_worlds:
    # This controls the allowed worlds to apply levels too.
    name: 'Excluded Worldlist'
    conditions:
      worlds:
        # allowed-list: ['*']
        excluded-list: [ 'world_the_end' ]
```

### Whitelist

If you want to use a *allowed-list*/*whitelist*, i.e., only worlds X, Y and Z are allowed to have levelled mobs, then use the following:

```yaml 
allowed-list: [ 'X', 'Y', 'Z' ]
# excluded-list: [ 'world_the_end' ]
```

Make sure `excluded-list` line has the comment symbol (`#`) so it is disabled.

### Blacklist

If you want to use a *excluded-list*/*blacklist*, i.e., all worlds except X, Y and Z are allowed to have levelled mobs, then use the following:

```yaml
# allowed-list: ['my_world']
excluded-list: [ 'X', 'Y', 'Z' ]
```

Make sure `allowed-list` line starts with the YAML comment symbol (`#`) so it is disabled.
 
</details>

## Why are LM's custom mob labels/nametags not being displayed?

<details>
<summary>See answer</summary>

> **Note:** This information does not pertain to LevelledMobs v3.5 or older, which requires ProtocolLib for 1.16-1.18 (and does not run on 1.19+). Keep your plugins and server software up-to-date!

* Running a MC 1.16, 1.17, or non-Paper-based 1.18 server? Make sure you install [ProtocolLib](https://www.spigotmc.org/resources/protocollib.1997/) in addition to LevelledMobs.
* Make sure there are no errors in your console, perhaps you have configured `rules.yml` incorrectly.
* Otherwise, labels should be displaying - if this is not the case, please contact support.

</details>

## How do I make Mob X a levelled mob?

### Also: Why are baby zombies, wardens, etc. not levelled?

<details>
<summary>See answer</summary>

By default, the following mobs are not levelled:

- Passive Mobs
- Baby Mobs (baby zombies, etc)
- Ravagers, Ender Dragons, Withers, Wardens
- Villagers, Zombie Villagers, Wandering Traders
- Phantoms and Bats

> **Note**: Mobs from spawners are also not levelled by default, we
have answered how to change this in another answer on the FAQ Wiki page.

Around line `399` in `rules.yml`, you should see something like this:

```yaml
custom-rules:
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

To make passive mobs levelled, change:

```yaml
allowed-groups: [ 'all_passive_mobs' ]
```

to:

```yaml
allowed-groups: []
```

To make one of the non-levelled mob types levelled, simply remove
it from the `allowed-list` line. For example, to make baby mobs
levelled, change:

```yaml
allowed-list: [ 'BABY_', 'ENDER_DRAGON', 'WITHER', 'VILLAGER', 'ZOMBIE_VILLAGER', 'WANDERING_TRADER', 'PHANTOM', 'BAT', 'RAVAGER', 'WARDEN' ]
```

to:

```yaml
allowed-list: [ 'ENDER_DRAGON', 'WITHER', 'VILLAGER', 'ZOMBIE_VILLAGER', 'WANDERING_TRADER', 'PHANTOM', 'BAT', 'RAVAGER', 'WARDEN' ]
```

How this area of rules.yml works by default, is that any mobs that pass the condition check (which checks their Entity Type e.g. `WITHER_SKELETON`),
are set to 'Level 0', i.e., they have no level.

</details>

## What levelling systems are available?

<details>
<summary>See answer</summary>
 
- **Weighted Random Levelling** (**default**)
    - Levels are a random number, but you can make certain level ranges more common than others.
    - By default, lower levels are more common than higher levels.
    - Comes with easy, normal, and hard mode presets.
- **Random Levelling**
    - Levels are a random number, each level has an equal chance of occurring.
- **Spawn-Distance Levelling**
    - Levels are based upon mobs' distance from their world's spawnpoint.
- **Y-Coord Levelling**
    - When mobs spawn, their level is based upon their current Y coordinate.
- **Blended Levelling**
    - Combines Spawn-Distance Levelling and Y-Coord Levelling together.
- **Player Levelling**
    - A special levelling system which allows you to use any player statistic from thousands of plugins (any PlaceholderAPI placeholder!) and make mobs levelled based upon that.
    - For example, you can make mobs have higher levels for players that have more EXP or money. All up to you!
    - We have an answer a few questions below this one where we explain in detail how you can use Player Levelling on your server.
- ... and more to come!

</details>

## How do I switch to another levelling system?

<details>
<summary>See answer</summary>

> **Note:** We have documented enabling the Player Levelling system for a separate question below, in case you were looking to enable that instead.

Find this area at the start of the default-rules section (your file may look slightly different):

```yaml
default-rule:
  use-preset:
    - allowed_worlds
    - nametag_using_numbers
    #- nametag_using_indicator
    #- basic_challenge
    - average_challenge
    #- advanced_challenge
    #- extreme_challenge
    - weighted_random_Levelling
    #- spawn_Levelling
    #- lvl-mod_spawn-blended
    #- ycoord_Levelling
    #- random_Levelling
    #- lvl-mod_player-variable
    #- lvl-mod_apply-variance
```

*Comment* out the levelling system you *don't* want to use, and *uncomment* the one you *want* to use.

> In YAML (`.yml`) files - the ones used in just about every plugin configuration - *commenting* refers to making a particular line begin with the `#` (hashtag) character. When the plugin reads the file, it ignores these comment lines.
>
> *'Why comment the line?'*: This allows you to keep the line without removing it, so you can easily re-enable the levelling strategy later.

Make sure you have one (1) nametag preset enabled, and one (1) challenge preset enabled, and one (1) levelling strategy enabled for this default rule.

Afterwards, run `/lm reload` or restart your server, so that your changes apply.

> **Note:** Existing mobs will not have their levels changed. You can run `/lm rules force_all` to force a rules evaluation for all entities in all worlds, taking any changes that have been made into account. You may alternatively choose to run `/lm kill all * /nodrops` in order to kill all levelled entities in all worlds without causing them to make any drops as well, allowing new ones to spawn into the world naturally.

> **Note:** Blended levelling requires Spawn-Distance Levelling to be enabled alongside it.

</details>

## Does LM change mob spawning mechanics / spawn rates?

<details>
<summary>See answer</summary>

**No, LevelledMobs does not change any spawn mechanics.** LevelledMobs only 'levels up' mobs that spawn. It doesn't spawn more mobs in, and it doesn't stop mobs from spawning. Zero spawning mechanics are altered. We are highly reluctant to change this behavior with LevelledMobs, as we don't like to introduce any obscure behaviours. :)

If you are having issues regarding mob spawning, configure your server software and/or anti-lag plugin.

</details>

## How do I make mobs from plugin X levelled / not levelled?

### Also: What is the `level-plugins` section?

<details>
<summary>See answer</summary>

From approximately [lines 327 to 399](https://github.com/ArcanePlugins/LevelledMobs/blob/master/src/main/resources/rules.yml#L327-L339) in `rules.yml`, you should see a section called `level-plugins`. This section has a list of supported plugins which are set to `false` by default. When you change any of these to `true`, newly spawned mobs from the respective plugin(s) are now considered for levelling by LevelledMobs.

For compatibility reasons, we recommend leaving all of these disabled. 

</details>

## What server software is supported?

<details>
<summary>See answer</summary>

See the [Compatibilities Wiki page](https://github.com/lokka30/LevelledMobs/wiki/Compatibilities).

</details>

## What plugins is LM compatible/incompatible with?

<details>
<summary>See answer</summary>

See the [Compatibilities Wiki page](https://github.com/lokka30/LevelledMobs/wiki/Compatibilities).

</details>

## How are attribute values calculated? (Formula)

<details>
<summary>See answer</summary>

The formula for each attribute value is:

```
newValue = defaultValue + ((defaultValue x configValue) x ((entityLevel - 1) / (maxLevel - 1)))
```

This formula will be simplified in the upcoming LevelledMobs 4.

</details>

## Will LM make my server lag?

<details>
<summary>See answer</summary>

Nope! We take performance seriously – for the few performance issues that have ever been reported and validated, all were promptly solved. We've worked with contributors to improve memory management, and run code asynchronously wherever useful.

</details>

## How do I use the Player Level Modifier?

<details>
<summary>See answer</summary>

> LM v3.8 renamed "Player Levelling" to "Player Level Modifier". 

### [If you wish to watch a video alternative to this section, click here!](https://www.youtube.com/watch?v=qTZ_GlQjGD8)

PLM is an add-on levelling system, which modifies the level of an entity based on a variable provided by the nearest player. It requires an actual levelling strategy to be enabled alongside this to function properly (for example, Weighted Random or Spawn-Distance Levelling), so that mobs have a baseline level until they are associated with a certain player. The default variable used for PLM is the exp level of the player, though any placeholder from PlaceholderAPI (PAPI) can be used, such as AureliumSkills, mcMMO, EcoSkills, and so on.

Below is the default preset used for Player Levelling, located in `rules.yml`.

```yaml
lvl-mod_player-variable:
# This Strategy Preset controls the player-variable based level modification system.
name: 'LVLling Modifier - Player Variable AVERAGE CHALLENGE'
strategies:
    player-levelling:
    match-level: true
    use-player-max-level: false
    decrease-level: true
    recheck-players: false
    preserve-entity: 10s
    player-level-scale: 1.0
    level-cap: 30
    tiers:
        1-15: 1-10
        16-30: 11-20
        31-45: 21-25
    variable: '%level%'
```

If you are going to use any other `variable`, you will want to set `match-level` and `use-player-max-level` to `false`, as they will override the `variable` settings. Refer to the
[wiki for Player Levelling](https://github.com/lokka30/LevelledMobs/wiki/Documentation---Strategies#player-variable-modifier)
regarding the various settings and their descriptions.

When you change the variable, you will need to understand what range of possible values that variable can produce. Your variable might only provide numbers as high as 50-100, or as high as 100,000 or more. If you're unsure of the value, you can use `/papi parse me <placeholder>`, replacing `<placeholder>` with the variable of your choosing. Once you understand the range of your `variable`, then you can adjust the possible `tiers`, which determine the potential levels that an entity will be adjusted to when near a player, based on the possible values of the `variable`. The values on the left side of `tiers` represent the potential values of the `variable`, while the values on the right side of `tiers` represent the potential level that LevelledMobs will adjust the entity to.

By default, LevelledMobs includes this preset within your `rules.yml` file in a disabled state. To enable this feature, you can locate the below section and enable the `- lvl-mod_player-variable` preset by removing the `#` before the line (uncommenting it). 

```yaml
default-rule:
  use-preset:
    - allowed_worlds
    - nametag_using_numbers
    #- nametag_using_indicator
    #- basic_challenge
    - average_challenge
    #- advanced_challenge
    #- extreme_challenge
    - weighted_random_Levelling
    #- spawn_Levelling
    #- lvl-mod_spawn-blended
    #- ycoord_Levelling
    #- random_Levelling
    - lvl-mod_player-variable
    #- lvl-mod_apply-variance
```

</details>

## How do I translate the names of entities/mobs?

<details>
<summary>See answer</summary>

> **Note:** There are several pre-made translations available in the
[Official Translations](https://github.com/lokka30/LevelledMobs/wiki/Official-Translations)
and
[Unofficial Translations](https://github.com/lokka30/LevelledMobs/wiki/Unofficial-Translations)
Wiki pages, which are ready to go!
There might be a translation for the language you want to translate the mob names to,
and the translations for your language might have entity names bundled too which you
can simply copy and paste into the `entity-name-override` section (see below for info on that).

See the `entity-name-override` section in `rules.yml`. This is at line `396` of the default `rules.yml` file, as of writing this answer.

> **Note:** The translation process has been significantly simplified in the upcoming LevelledMobs 4. :)

</details>

## Does LevelledMobs make higher level mobs drop more/better items/XP?

<details>
<summary>See answer</summary>

By default, LevelledMobs will multiply the item and experience orb drops on levelled mobs, where higher level mobs will drop more of them. You can customise the drops using our Custom Drops system.

</details>

## How does LevelledMobs work?

<details>
<summary>See answer</summary>

Here is a short explanation for laymen:

When mobs spawn on your server, LevelledMobs checks if they should be levelled. If they pass this inspection, then LevelledMobs will generate and assign a number to the mob (their 'level'). This level determines various qualities about the mob, such as the increase in strength and speed for higher level mobs. You can customise LevelledMobs to great extents, such as by adding your own custom drops for levelled mobs, and so much more!

</details>

## How do I change the label/nametag format?

<details>
<summary>See answer</summary>

Firstly, let's check which nametag type preset you are using.

Open up `rules.yml` and scroll down to the `use-presets` section for your `default-rule`.
As of writing, this is approximately line `348`.

You should see a section that looks similar to this:
```yaml
default-rule:
  use-preset:
    - allowed_worlds
    - nametag_using_numbers
    #- nametag_using_indicator
    ...
    ...
    ...
```

Now, the nametag preset you are using is either `nametag_using_numbers` or `nametag_using_indicator`,
whichever one is ***not*** commented out. By default, this is `nametag_using_numbers`.

Now that you know which nametag preset you're using, scroll up to the area where such preset is configured.
As of writing, this is either line `310` (for `nametag_using_indicator`), or line `328` (for `nametag_using_numbers`).

You should see a section that looks similar to this:
```yaml
nametag_using_indicator:
    name: 'Nametag - Health Indicator'
    apply-settings:
        nametag: '&8&l༺ %tiered%Lvl %mob-lvl%&8 | &f%displayname%&8 | &f%entity-health-rounded% %tiered%%heart_symbol% &r%health-indicator% &8&l༻'
        health-indicator:
            ...
            ...
            ...
            merge: true

nametag_using_numbers:
    name: 'Nametag - Health Numerical'
    apply-settings:
        nametag: '&8&l༺ %tiered%Lvl %mob-lvl%&8 | &f%displayname%&8 | &f%entity-health-rounded%&8/&f%entity-max-health-rounded% %tiered%%heart_symbol% &8&l༻'
```

Simply edit the value of the relevant `nametag` option to customise the format. Then, run `/lm reload`
(or restart your server) to apply the changes. 

</details>

## How do I edit mob drops?

<details>
<summary>See answer</summary>

Check out `customdrops.yml`. That file is documented [here](https://github.com/lokka30/LevelledMobs/wiki/Documentation---customdrops.yml).

</details>

## How do I change the difficulty of levelled mobs?

#### Also: What are Challenges, and how can they be modified?

<details>
<summary>See answer</summary>

We have prepared 4 different "challenges" for our users. Challenges are essentially a difficulty level that only affects levelled mobs, being completely independent from your server's difficulty (e.g. 'hard').

By default, the 'Average' challenge is used, which is intended to create levelled mobs as if Minecraft had a 'harder' difficulty. You can use the
'basic' challenge to create mobs that are easier to fight, or any of the two harder challenges ('advanced' and 'extreme'). You can even create your
own or modify the ones we have created for you.

Around line `350` in the `rules.yml` file, you can select which "challenge" preset you would like to use. It looks like this by default:

```yaml
#- basic_challenge
- average_challenge
#- advanced_challenge
#- extreme_challenge
```

Changing the one you want to use is akin to selecting a different levelling system. Make sure you have one (1) challenge enabled (no more, no less) at
any given time. Disable the average challenge by adding a comment character (`#`) to the start of its line, and uncomment (remove the `#` character) the
line of the challenge you want to use instead. For example, if you wanted to use the basic challenge, it should look like this:

```yaml
- basic_challenge
#- average_challenge
#- advanced_challenge
#- extreme_challenge
```

If you are not satisfied with the challenges we have prepared, we suggest duplicating an existing challenge preset, modifying it, and then enabling it
in the default rule area (add a line just like the other challenges). For example, to add an 'Insane Challenge' which is harder than 'extreme':

1. From approx. lines `236` to `267` is the `extreme_challenge` preset. Duplicate that entire preset and rename the new, duplicate preset to `insane_challenge`.

2. Edit the values to your liking. Multipliers follow a formula which we have documented in another answer on the FAQ Wiki page. Support may be available
on our Discord for modifying these values. We recommend using a test server to experiment with values until you are fully satisfied with the outcome.

3. At approx. lines `311` to `314` (in your default rule's `use-presets` section), add make sure all other challenges are commented out, and add the `insane_challenge` line (and make it enabled):

```yaml
#- basic_challenge
#- average_challenge
#- advanced_challenge
#- extreme_challenge
- insane_challenge
```

4. Save the file.

5. Optional: run `/lm rules force_all` to make the new difficulty
apply to existing levelled mobs on your server. This will re-level every loaded entity.

</details>

## How do I make mobs from Monster Spawners levelled?

<details>
<summary>See answer</summary>

> **Note**: We have chosen to not make mobs from spawners levelled by
default to keep things balanced. We recommend you make spawner mobs
not have drop bonuses. We also recommend that spawner mobs do not
have their health changed if you wish to not break mob farms that rely
on fall damage.

Approximately line `325` in `rules.yml`, in the `allowed-spawn-reasons` section, change:

```yaml
conditions:
    allowed-spawn-reasons:
        excluded-list: [ 'SPAWNER' ]
```

to:

```yaml
conditions:
    allowed-spawn-reasons:
        excluded-list: []
```

This will make all mobs from Monster Spawners have a level.

</details>

## How do I exclude nametagged mobs from levelling?

<details>

<summary>See answer</summary>

Look in your rules.yml for the following:
```yaml
mob-customname-status: EITHER
```
The line number will vary depending on your rules version but should be around line 347.
Update it to:
```yaml
mob-customname-status: NOT_NAMETAGGED
```
Save your file then run command `/lm rules force_all`

</details>

## How do I change the max level?

<details>
<summary>See answer</summary>

Firstly, let's determine what Challenge preset you are using.

From approximately line `311` to `314` in `rules.yml`, you should see something like this - you might have adjusted it, and that's fine:

```yaml
#- basic_challenge
- average_challenge
#- advanced_challenge
#- extreme_challenge
```

Notice how in this example (default file) has the `average_challenge` preset enabled. This preset is defined around line `212` in `rules.yml`. If you
are not using the average challenge then you will need to modify a different preset instead, e.g. modify the `basic_challenge` preset if you are using
the basic challenge.

For those using the average challenge, you should see something like this around line `175`:

```yaml
  average_challenge:
    name: 'Average-Challenge Multipliers'
    apply-settings:
      minLevel: 1
      maxLevel: 25
      multipliers:
        max-health: 5.0
        movement-speed: 0.15
        attack-damage: 2.25
        ranged-attack-damage: 2.25
        creeper-blast-damage: 0.7
        #... continues ...
```

Change `maxLevel` (in this case, currently `25`) to whichever value you like. We recommend using a reasonable value such as `50`, `100`, or `1000`, but
LM gives you the power to choose whichever value you want.

Once your edit is done, save the file. We highly recommend running `/lm rules force_all` to relevel all mobs on your server so that they reflect the
new max level. It would be weird to have level 25s roaming around which seem to have the same strength as a level 100. :)

</details>

## How do I make custom drops from other plugins such as ExecutableItems, ItemsAdder and EcoItems?

<details>
<summary>See answer</summary>

Use PenalBuffalo's [LM Items](https://www.spigotmc.org/resources/lm-items.102081/) addon plugin.

</details>

## How can I increase attributes (e.g. health) of mobs past 2048?

<details>
<summary>See answer</summary>

LevelledMobs does not limit this value, it's your server software.

In `spigot.yml`, increase the attribute max values:

```yaml
  attribute:
    maxHealth:
      max: 2048.0
    movementSpeed:
      max: 2048.0
    attackDamage:
      max: 2048.0
```

Note that Minecraft's attribute system was not designed for insanely high values, be careful if you are going to raise the limits very high.

</details>

## Does LevelledMobs apply levels to Players too?

<details>
<summary>See answer</summary>

No it does not. This plugin is designed to only level mob-like entities, and we have no intentions of adding a player component. There are many alternatives which are far more refined for Players such as [AureliumSkills (Free)](https://www.spigotmc.org/resources/aurelium-skills-advanced-skills-stats-abilities-and-more.81069/) or [McMMO (Paid)](https://www.spigotmc.org/resources/official-mcmmo-original-author-returns.64348/). 

</details>

## MythicMob entities are not levelling/scaling properly?

<details>
<summary>See answer</summary>

Around MythicMobs version 5.2.6 there was a change made in the default configuration of the MythicMobs installation which enables by default the scaling/levelling of entities via their own mechanics that are entirely separate from LevelledMobs. LevelledMobs detects a fully created entity and then applies levels to that entity; if MythicMobs' has their scaling system active that will mean they will start with varied and increasing stats before LevelledMobs even has a chance to adjust them.

In order to reset entities to their vanilla stat values, you could disable the scaling system within MythicMobs to use LevelledMobs' levelling exclusively, or vice-versa (of course we recommend using ours over theirs but it's your choice!). To disable, locate the `config.yml` file in your MythicMobs' installation, and set the `Enabled:` under each respective worlds/scenarios to `false` to disable the scaling of MythicMobs for those scenarios. You can also adjust the Modifiers themselves to allow for some scaling controlled by MythicMobs.

![MM Config.YML](https://i.ibb.co/KV2jsP9/image.png)

</details>


## Your question not listed?
Please ask our staff on the
[ArcanePlugins Discord Server](https://www.discord.io/arcaneplugins).