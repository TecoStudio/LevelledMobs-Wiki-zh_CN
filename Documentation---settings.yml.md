```
This page was last updated for LevelledMobs 3.9.3 b735
```

---

# Should LM stop sending packets if an entity has died?

```yaml
assert-entity-validity-with-nametag-packets: true
```

* `true` - Once an entity has reached zero health, packets for that entity will no longer be sent.

* `false` - Once an entity has reached zero health, LM may send extra packets to try make sure the entity's nametag data (such as their health) is accurate.

This setting attempts to fix a compatibility issue with ViaBackwards where VB detects LM sending name tag packets of entities which are dead.  

It is not recommended that you change this setting unless you understand exactly what you are doing.

<br /><br />

# Automatic Asynchronous Nametag and Level Updater

```yaml
async-task-update-period: 6
async-task-max-blocks-from-player: 100
```

This setting will check the the area within X blocks of a player, where X is the `async-task-max-blocks-from-player:`, for any entities which should have been levelled, LM nametagged, or are missing attributes for whatever reason.  

The `async-task-update-period:` is counted in seconds.

<br /><br />

# Customize Summon Command Limit

```yaml
customize-summon-command-limit: 10
```

This setting will forcibly limit the number of entities which can be summoned with LM's `/lm summon` command per use.

This is used to help prevent any accidents or overloading your server with countless entity summons.

<br /><br />

# Head Drop Multiplier

```yaml
mobs-multiply-head-drops: false
```

* `true` - Mob head item drops **will not** be multiplied if they otherwise would be.
* `false` - Mob head item drops **will** be multiplied as if they were any other material drop.

On some servers, heads are considered too valuable of a resource to be multiplied alongside the other drops of an entity. This setting allows you to decide whether you want to allow these drops to multiply alongside everything else that would have dropped.

<br /><br />

# Customize Command Drop Limiters

```yaml
customcommand-amount-limit: 100
```

This helps to prevent any accidental crashes through an entity running more commands than your server can handle upon death. This will set a hard-limit on any custom commands dropped through the Custom Drops system, overriding any set `amount:` which is above this value.

<br /><br />

# Mob Processing Delay

```yaml
mob-process-delay: 0
```

This will add an additional amount of delay, counted in ticks, before LM begins to process the entity. Adding delay is only useful in situations where other plugins need time to process before LM applies any values.

It is not recommended that you change this setting.

<br /><br />

# Summon Command Spawn-Distance-from-Player

```yaml
summon-command-spawn-distance-from-player: 5
```

This will determine how far away from a player an entity will spawn when you utilize `/lm summon <quantity> <entity> <level> here`.

<br /><br />

# Kill-Skip Conditions

```yaml
kill-skip-conditions:
  nametagged: true
  tamed: true
  leashed: true
  convertingZombieVillager: true
```

For each kill-skip condition above:

* `true` - Entities under that condition **will** be skipped during LM's kill command.
* `false` - Entities under that condition **will not** be skipped during LM's kill command.

These will specify what entities are skipped when you utilize `/lm kill`.

This is useful to prevent any pets or other unintended entity deaths.

It is recommended that you do not adjust these settings without knowing what you are doing.

<br /><br />

# Use Translation Components

```yaml
use-translation-components: true
```

* `true` - Any default entity names will be displayed to the player in the native language used in the players' client.
* `false` - Some older and customized clients do not support this feature, so you may disable this if your servers' environment requires this circumvention. 

This system provides a quality of life mechanism and should be enabled in most situations; this feature does not exist in older Minecraft clients and some customized clients, and can result in broken names being displayed to the player. Should your server necessitate this kind of circumvention, then by disabling this feature you are instead referencing an internal table of English names. You can still modify the name of entities via the `apply-setting: entity-name-override:` feature of the `rules.yml`.

<br /><br />

# Verify Entities on Chunk Load

```yaml
ensure-mobs-are-levelled-on-chunk-load: true
```

* `true` - Loaded chunks nearby players will be checked for any entities which are missing a level which should not be.
* `false` - Entities which were not levelled for whatever reason will not be double-checked.

This system acts like a janitor, checking loaded chunks nearby players for any entities which should be levelled and are not.

It is recommended that you do not change this setting if you do not understand its effects.

<br /><br />

# Attributes Use Preset Base-Values

```yaml
attributes-use-preset-base-values: false
```

* `true` - Use the static, predefined entity attribute values.
* `false` - Collect the attributes from the spawned entity itself.

In LM v2, we used a static file to generate the entity attributes. This helped to eliminate compatibility issues that existed at the time. Since then, we have significantly changed how attributes are gathered and modified. With that in mind, we decided to offer the static file as a backup solution in case future issues arise. It is not recommended that you alter this setting.

<br /><br />

# Use 'CustomName' for Entity Nametags

```yaml
use-customname-for-mob-nametags: false
```

* `true` - Use the entity's `CustomName` field for the LM nametag.
* `false` - Fake LM's nametag using packets through the ProtocolLib plugin.

Prior to LM v2, we used the **real** nametag associated with entities when applying the LM nametag. This caused conflicts with other plugins, and was overriden when players put name tags on mobs.

Since LM v2, we now fake the effect using packets through the ProtocolLib plugin. It factors in players using nametags and such.

As a backup solution we have this config which allows you to revert to a very similar process which LM v1 used to process nametags. It is not recommended that you alter this setting.

**This setting is irreversible!**

<br /><br />

# Level Entities on Spawn

```yaml
level-mobs-upon-spawn: true
```

* `true` - Once an entity has been spawned into the world, LM will immediately attempt to apply a level to the entity.
* `false` - Entities will not receive a level until they either take damage from a player or have targeted a player.

<br /><br />

# Chunk Kill Count System

```yaml
exceed-kill-in-chunk-message: true
```

* `true` - When the chunk kill count system is enabled and reaches the threshold for max deaths a chunk, a message will be sent to the player that killed the mob.
* `false` - No messages will be sent to any players for the chunk kill count system.

<br /><br />

# Player Levelling Strategy Settings

```yaml
player-levelling-relevel-min-time: 5000
```

`player-levelling-relevel-min-time:` represents the time, in milliseconds, before an entity is updated against the nearest player. Setting this to `0` will prevent any relevelling. 

These settings revolve around the levelling strategy known as **Player Levelling**.

<br /><br />

# Nametag Placeholder Distance

```yaml
nametag-placeholder-maxblocks: 30
```

`nametag-placeholder-maxblocks:` represents the the maximum distance from the player an entity can be to be registered under `%levelledmobs_mob-target%`.

<br /><br />

# Updates and Debug Settings

```yaml
use-update-checker: true
debug-entity-damage: false
debug-misc: [ '' ]
file-version: 30
```

`use-update-checker:` When set to `true`, this will notify you once at server startup whether you have an up-to-date version of LM.

`debug-entity-damage:` When set to `true`, this will display detailed attribute information in-game when you hit an entity.

`debug-misc:` Refer to [settings.yml/Debug-Misc](https://github.com/lokka30/LevelledMobs/wiki/Documentation---Debug-Misc) for further details.

`file-version:` This value represents the config processing version. Do not alter this value, or you may break your plugin and configs.