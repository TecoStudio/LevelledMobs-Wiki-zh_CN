LevelledMobs allows you to level mobs based upon nearby players' statistics.
These statistics are gathered by using any PlaceholderAPI placeholder of your choice.

## 1. Find a placeholder to use

Since you're using EcoSkills, you can use any of EcoSkills' placeholders:

<https://plugins.auxilor.io/ecoskills/placeholderapi>

## 2. Configure Player Levelling

Find the `player_Levelling` preset in `rules.yml`:

```yaml
  player_Levelling:
#   This Strategy Preset controls the player-stat based levelling system.
    name: 'LVLling Strategy - Player Based AVERAGE CHALLENGE'
    strategies:
      player-levelling:
        match-level: true
        use-player-max-level: false
        decrease-level: true
        player-level-scale: 1.0
        level-cap: 30
        tiers:
          1-15: 1-10
          16-30: 11-20
          31-45: 21-25
        variable: '%level%'
```

Then, edit the `variable` option to use the placeholder you wish.

> Tip: you can use PlaceholderAPI's 'Maths' module to effectively use multiple placeholders together. :)

Feel free to customize the other options as you wish. All of the Player Levelling options are explained on our Wiki:

<https://github.com/lokka30/LevelledMobs/wiki/Documentation---Conditions,-Strategies,-and-Apply-Settings#player-levelling>

Lastly, scroll down to the `default-rule` section and enable Player Levelling ...

Your `default-rule`'s `use-preset` area should look like this:

```yaml
default-rule:
  use-preset:
    - allowed_worlds
    - nametag_using_numbers
#    - nametag_using_indicator
#    - basic_challenge
    - average_challenge
#    - advanced_challenge
#    - extreme_challenge
#    - apply_LevellingVariance
#    - weighted_random_basic
    - weighted_random_average
#    - weighted_random_advanced
#    - weighted_random_extreme
#    - spawn_Levelling
#    - blended_Levelling
#    - ycoord_Levelling
#    - random_Levelling
#    - player_Levelling
```

Change it to look like this:

```yaml
default-rule:
  use-preset:
    - allowed_worlds
    - nametag_using_numbers
#    - nametag_using_indicator
#    - basic_challenge
    - average_challenge
#    - advanced_challenge
#    - extreme_challenge
#    - apply_LevellingVariance
#    - weighted_random_basic
    - weighted_random_average
#    - weighted_random_advanced
#    - weighted_random_extreme
#    - spawn_Levelling
#    - blended_Levelling
#    - ycoord_Levelling
#    - random_Levelling
    - player_Levelling
```

Remember to save your changes to the file (`File` -> `Save`).

## 3. Reload and re-level mobs

Now that you have told LevelledMobs to use Player Levelling, let's reload it so that LM knows to check your file for changes.

The following command will also re-level all known levelled mobs on your server, so that they can use the Player Levelling system. :)

Run: `/lm rules force_all`

## Done!

Mobs should now be levelled based on your chosen EcoSkills statistic. :)
