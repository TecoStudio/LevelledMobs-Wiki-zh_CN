```
This page was last updated for LevelledMobs v3.1.2 b486
```

***

Here are the list of permissions you can utilize with an installed permissions plugin.

We highly recommend [LuckPerms](https://luckperms.net/), but LevelledMobs doesn't care which permissions plugin you use :)

***

Columns:
* `Permission`: the permission label you assign to users &/or groups using a permissions management plugin.
* `Default Ownership`: shows which players have the permission by default.
  * `Everyone`: all players have the permission by default.
  * `Operators`: players with operator status (from `/op`) have the permission by default.
  * `Nobody`: no players have the permission by default.
* `Description`: a short description about what the permission gives users access to.

***

<table>
    <tr>
        <th>Permission</th>
        <th>Default Ownership</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>levelledmobs.*</td>
        <td>Operators</td>
        <td>Access to all LevelledMobs permissions.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.*</td>
        <td>Operators</td>
        <td>Access to all LevelledMobs commands permissions.</td>
    </tr>
    <tr>
        <td>levelledmobs.command</td>
        <td>Everyone</td>
        <td>Access to the base command, `/levelledmobs`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.summon.*</td>
        <td>Operators</td>
        <td>Access to all `/levelledmobs summon` permissions.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.summon</td>
        <td>Operators</td>
        <td>Access to `/levelledmobs summon`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.summon.bypass-level-limit</td>
        <td>Operators</td>
        <td>Makes LevelledMobs ignore the levels specified in `/levelledmobs summon` if they are above the level limit in your configuration.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.kill.*</td>
        <td>Operators</td>
        <td>Access to all `/levelledmobs kill` permissions.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.kill</td>
        <td>Operators</td>
        <td>Access to `/levelledmobs kill`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.kill.all</td>
        <td>Operators</td>
        <td>Access to `/levelledmobs kill all`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.kill.near</td>
        <td>Operators</td>
        <td>Access to `/levelledmobs kill near`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.reload</td>
        <td>Operators</td>
        <td>Access to `/levelledmobs reload`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.info</td>
        <td>Everyone</td>
        <td>Access to `/levelledmobs info`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.compatibility</td>
        <td>Operators</td>
        <td>Access to `/levelledmobs compatibility`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.spawner.*</td>
        <td>Operators</td>
        <td>Access to all `/levelledmobs spawner` commands.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.spawner</td>
        <td>Operators</td>
        <td>Access to `/levelledmobs spawner`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.spawner.copy</td>
        <td>Operators</td>
        <td>Access to `/levelledmobs spawner copy`.</td>
    </tr>
    <tr>
        <td>levelledmobs.command.rules</td>
        <td>Operators</td>
        <td>Access to `/levelledmobs rules`.</td>
    </tr>
    <tr>
        <td>levelledmobs.debug</td>
        <td>Operators</td>
        <td>Ability to utilise debug functionality, if enabled in the settings file.</td>
    </tr>
    <tr>
        <td>levelledmobs.compatibility-notice</td>
        <td>Operators</td>
        <td> Ability to view the compatibility notice on join if any possible incompatibilities are found on startup.</td>
    </tr>
    <tr>
        <td>levelledmobs.receive-update-notifications</td>
        <td>Operators</td>
        <td>Receive update checker notifications in chat on join, if enabled.</td>
    </tr>
</table>