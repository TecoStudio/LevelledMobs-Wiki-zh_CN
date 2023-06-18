```
This page was last updated for LevelledMobs 3.2.0 b520
```

***

The following commands are available for LevelledMobs purposed for administrators to manage the plugin and existing levelled mobs in your worlds.

***

To view the permissions in more depth, please see the Permissions page of this wiki.

* `/levelledmobs`
  * Base command of the plugin. Running it without supplying any arguments will return a list of commands you can use.
  * Requires permission `levelledmobs.command`

# /levelledmobs rules
  * `force_all`                - forces all mobs to be reevaluated by LevelledMobs
  * `help_discord`             - shows the link to join Arcane Plugins Discord
  * `help_wiki`                - shows the link for this wiki
  * `reset <easy/normal/hard>` - resets the rules.yml with a predefined difficulty
  * `show_all`                 - shows all rules as configured in rules.yml
  * `show_effective`           - shows current rules applicable to the mob closest to you
  * `show_rule <name>`         - shows the specified rule

# /levelledmobs spawner
* `/levelledmobs spawner create`
  * Creates a spawner in your inventory that will only spawn mobs within the specified min and max range.  You'll need to place an egg of the mob you want the spawner to use if you don't specify spawntype in the arguments below.
  * Arguments.  Use any combination of the following arguments.  Most are optional:
    * `/minlevel <number>`           - mobs will be spawned with this level as the minimum
    * `/maxlevel <number>`           - mobs will be spawned with this level as the maximum
    * `/name <name>`                 - gives the spawner the specified custom name
    * `/lore <lore>`                 - sets the specified lore. use `\n` for multiple lines
    * `/nolore`                      - removes the default lore
    * `/customdropid <id>`           - will use the specified droptableid in customdrops.yml for any mobs spawned from this spawner
    * `/spawntype <type>`            - sets the spawner's creature type.
    * `/delay <number>`               - sets the spawner's delay
    * `/maxnearbyentities <number>`   - sets the maximum number of similar entities that are allowed to be within spawning range of this spawner
    * `/minspawndelay <number>`       - sets the minimum spawn delay amount (in ticks)
    * `/maxspawndelay <number>`       - sets the maximum spawn delay amount (in ticks)
    * `/requiredplayerrange <number>` - sets the maximum distance (squared) a player can be in order for this spawner to be active
    * `/spawncount <number>`          - sets how many mobs attempt to spawn
    * `/spawnrange <number>`          - set the new spawn range
    * `/giveplayer <player>`          - gives the spawner to the specified player

* `/levelledmobs spawner info` - shows you information about LM spawners by right-clicking on them
    * run without arguments to show if it is enabled or not.
    * `on`  - enables spawner info mode
    * `off` - disables spawner info mode

* `/levelledmobs spawner copy` - allows you to duplicate a LM spawner by right-clicking on it
    * run without arguments to show if it is enabled or not.
    * `on`  - enables spawner copy mode
    * `off` - disables spawner copy mode

# /levelledmobs eggs
  * Arguments.  minlevel, maxlevel and spawntype are required.  The rest are optional.
    * `/minlevel <number>`           - mobs will be spawned with this level as the minimum
    * `/maxlevel <number>`           - mobs will be spawned with this level as the maximum
    * `/name <name>`                 - gives the spawner the specified custom name
    * `/lore <lore>`                 - sets the specified lore. use `\n` for multiple lines
    * `/nolore`                      - removes the default lore
    * `/customdropid <id>`           - will use the specified droptableid in customdrops.yml for any mobs spawned from this spawner
    * `/spawntype <type>`            - sets the spawner's creature type.
    * `/giveplayer <player>`          - gives the spawner to the specified player

# /levelledmobs summon
  * Similar to Minecraft's `/summon` command, this spawns in a levelled mob of your specification. For example, you can spawn a **Level 1 Zombie** at **Notch**'s location, or 5 blocks above your head.
  * Requires permissions `levelledmobs.command` and `levelledmobs.command.summon`
  * Usages (self-explanatory)
    * `/levelledmobs summon <amount> <entity> <level> here`
    * `/levelledmobs summon <amount> <entity> <level> atPlayer <player>`
    * `/levelledmobs summon <amount> <entity> <level> atLocation <x> <y> <z> [world]`

# /levelledmobs kill
  * Similar to Essentials' `/killall` command, this kills only levelled mobs nearby or all in the world of your specification.
  * Requires permissions `levelledmobs.command` and `levelledmobs.command.kill`, plus an extra permission for each subcommand found below in the Usages section.
  * Usages:
    * `/levelledmobs kill all [world/*]`
      * This kills all levelled mobs in the sender's world or the specified world. If the `*` character is specified in the world argument, then it will kill all levelled mobs in all worlds loaded on the server.
      * Requires additional permission `levelledmobs.command.kill.all`
    * `/levelledmobs kill near <radius>`
      * This kills all levelled mobs within the radius of the sender.
      * Requires additional permission `levelledmobs.command.kill.near`

# /levelledmobs reload
  * Similar to a lot of plugins' `reload` subcommands, this simply reloads the configuration files from the disk to apply its changes without having to restart your server.
  * Requires permissions `levelledmobs.command` and `levelledmobs.command.reload`

# /levelledmobs debug
  * This initiates the Debug branch of LevelledMobs. In the future, you will be able to enable and disable Debug options via command instead of through the `settings.yml` file alone.
  * Check back for updates!

# /levelledmobs info
  * This subcommand prints information about the version of the plugin installed, including its name, version, author, description, list of supported Minecraft versions and the great code contributors that also made this plugin possible.

# /levelledmobs compatibility
  * This subcommand runs the compatibility checker. Simply check the console logs to see if your server may be missing significant features or running an unsupported configuration.
  * Requires permissions `levelledmobs.command` and `levelledmobs.command.compatibility`