```
This page was last updated for LevelledMobs 3.9.1 b730
```

***

# Debug-Misc

```yml
debug-misc: [ '' ]
```

These are all of the potential debug options to input into the `debug-misc:` config line located within `settings.yml`.

You can use multiple debug options, separated by commas. 

> ### Denied Levelling<br />
> Options related to any flags which denied an entity a level.
* `APPLY_LEVEL_FAIL` - Reports when LM does not apply a level to an entity.
* `ENTITY_TRANSFORM_FAIL` - Reports when an entity that has 'transformed' was not eligable for a level.
* `SCOREBOARD_TAGS` - Reports a level being denied due to a scoreboard tags rule not meeting criteria.
* `SKYLIGHT_LEVEL` - Reports a level being denied due to the skylight level rule not meeting criteria.
* `DENIED_FORCE_BLOCKED_ENTITY_TYPE` - When LM does not apply a level due to a hardcoded entity type.
* `DENIED_RULE_ENTITIES_LIST` - Reports a level being denied due to exclusion from entity list.
* `DENIED_RULE_MINLEVEL` - Reports a level being denied due to the minimum not being reached.
* `DENIED_RULE_MAXLEVEL` - Reports a level being denied due to the value being over maximum.
* `DENIED_RULE_WORLD_LIST` - Reports a level being denied due to an entity spawning in an excluded world list.
* `DENIED_RULE_BIOME_LIST` - Reports a level being denied due to an entity spawning in an excluded biome list.
* `DENIED_RULE_PLUGIN_COMPAT` - Reports a level being denied due to a specific plugin being excluded.
* `DENIED_RULE_SPAWN_REASON` - Reports a level being denied due to a specific excluded `allowed-spawn-reason:`.
* `DENIED_RULE_CUSTOM_NAME` - Reports a level being denied due to the `CustomName` matching a configured value.
* `DENIED_RULE_CHANCE` - Reports a level being denied due to random chance configuration.
* `DENIED_RULE_WG_REGION` - Reports a level being denied due to the rules of a `WorldGuard` region.
* `DENIED_RULE_WG_REGION_OWNER` - Reports a level being denied due to the rules of a `WorldGuard` region's owner.
* `DENIED_RULE_MYTHIC_MOBS_INTERNAL_NAME` - Reports a level being denied due to a condition check against the MM entity name.
* `DENIED_RULE_RULE_Y_LEVEL` - Reports a level being denied due to the entity's position being above or below a specific Y-Coordinate configured.
* `DENIED_LEVEL_0` - Reports a level being denied due to `maxLevel: 0` set for that entity.
* `DENIED_RULE_MIN_SPAWN_DISTANCE` - Reports a level being denied due to being too close to spawn.
* `DENIED_RULE_MAX_SPAWN_DISTANCE` - Reports a level being denied due to being too far from spawn.
* `DENIED_RULE_RULE_STOP_PROCESSING` - Reports a level being denied due to the `stop-processing:` config option.
* `DENIED_RULE_SPAWNER_NAME` - Reports a level being denied due to the spawner name not meeting criteria.
* `DENIED_RULE_WORLD_TIME_TICK` - Reports a level being denied due to the world time tick not meeting criteria.
* `DENIED_RULE_PERMISSION` - Reports a level being denied due to the user permissions not meeting criteria.
* `DENIED_RULE_WITH_COORDINATES` - Reports a level being denied due to it being outside of a specified `within-coordinates:` location.

> ### Pre-Processing<br />
> Options related to processes handled prior to a level being successfully applied to an entity.
* `ENTITY_SPAWN` - Reports when an entity has spawned and LM has taken over.

> ### Rules Processing<br />
> Options related to processes handled on a listener or cooldown, connected to the Rules system.
* `APPLY_LEVEL_SUCCESS` - Reports when LM applied a level to an entity successfully.
* `MOB_SPAWNER` - Reports entities which have been levelled from a Spawner Cube.
* `ENTITY_MISC` - Reports when a baby entity ages into an adult, and is eligable to be levelled.
* `PLAYER_LEVELLING` - Shows debug information relating to the `Player Levelling` strategy, if utilized.
* `ATTRIBUTE_MULTIPLIERS` - Shows debug information relating to how the attributes are being multiplied.
* `NBT_APPLY_SUCCESS` - Reports when NBT data was successfully applied to a levelled entity.
* `RULE_COOLDOWN` - Reports a rule has been disabled due to it meeting the cooldown criteria.
* `MULTIPLIER_REMOVED` - Reports when a `vanilla-bonus:` is removed from an entity.

> ### Post-Processing<br />
> Options related to processes handled once an entity has been levelled.
* `ENTITY_TAME` - Reports when a levelled entity has been tamed.
* `RANGED_DAMAGE_MODIFICATION` - Reports the adjusted ranged damage output from projectiles which have caused damage.

> ### On-Death Processing<br />
> Options related to processes handled once a levelled entity has died.
* `CUSTOM_DROPS` - Reports when a `CustomDrop` from LM has been processed.
* `CUSTOM_COMMANDS` - Reports when a `CustomCommand` from the `CustomDrop` system has been processed.
* `SET_LEVELLED_ITEM_DROPS` - Reports when LM adjusts an entity's item drops.
* `SET_LEVELLED_XP_DROPS` - Reports when LM adjusts an entity's experience drops.
* `CHUNK_KILL_COUNT` - Reports when a chunk has met the max criteria to disable drops.

> ### Developer Options<br />
> Options meant for developers only. 
* `THREAD_LOCKS` - Shows debug information relating internal thread locks.
