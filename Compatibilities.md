```
This page was last updated for LevelledMobs 3.10.1
```

***

In this Wiki page, you'll find out if your server is compatible with LevelledMobs.

> **Note:** *"Supported"* refers to whether or not the LevelledMobs support staff are willing to help you out with issues with the plugin.

> **Note:** *"Compatibility"* refers to what degree the LevelledMobs plugin can run without issues or missing features.

# Minecraft Versions

**Minecraft versions which are *not* listed in the table below are *not* compatible or supported.**

> **Note:** *Not running the latest Minecraft version?* You're missing out on a large pool of potential players, exploit patches, bug fixes, new features, performance improvements, plugin availability, plugin support, and community support. Get updated. ;)

> **Warning:** `LM v4.0.0`, a future revamp version of LevelledMobs, will require the latest version of MC.

<table width="100%">
    <tr>
        <th>MC Version</th>
        <th>Compatibility</th>
        <th>Support</th>
        <th>Minimum Java Ver</th>
        <th>Comment</th>
    </tr>
    <tr>
        <td>1.18.x, 1.19.x, 1.20.x</td>
        <td>🟢</td>
        <td>🟢</td>
        <td>17</td>
        <td></td>
    </tr>
    <tr>
        <td>1.17.x</td>
        <td>🟢</td>
        <td>🟢</td>
        <td>17</td>
        <td>
            If you're not running Paper (or a fork/derivative of it), you'll need to install the <a href="https://www.spigotmc.org/resources/protocollib.1997/">ProtocolLib</a> plugin as well.
        </td>
    </tr>
    <tr>
        <td>1.16.x</td>
        <td>🟢</td>
        <td>🟢</td>
        <td>17</td>
        <td>
            You'll need to install the <a href="https://www.spigotmc.org/resources/protocollib.1997/">ProtocolLib</a> plugin too.
            <br/>
            If your PaperMC server isn't starting due to the Java version, try adding the <code>-DPaper.IgnoreJavaVersion=true</code> flag.
            <br />
            <i>Our support staff can't assist you with Java version issues.</i>
        </td>
    </tr>
</table>

# Server Software

**Server software which is *not* listed in the table below is *not* supported (nor guaranteed to be compatible).**

<table width="100%">
    <tr>
        <th>Server Software</th>
        <th>Compatibility</th>
        <th>Support</th>
        <th>Comment</th>
    </tr>
    <tr>
        <td>PaperMC</td>
        <td>🟢</td>
        <td>🟢</td>
        <td>Reference software; recommended</td>
    </tr>
    <tr>
        <td>PurpurMC</td>
        <td>🟢</td>
        <td>🟢</td>
        <td></td>
    </tr>
    <tr>
        <td>SpigotMC</td>
        <td>🟡</td>
        <td>🟢</td>
        <td>
            Slightly limited compatibility; some features in LM require <a href="https://papermc.io/">PaperMC</a> (or a derivative/fork).
        </td>
    </tr>
</table>

### Do not use 'Hybrid' server software!

> **Note:** 'Hybrid' server software means that the server software can run Bukkit plugins in addition to Forge/Fabric mods.

Mohist, Arclight, Cauldron, Magma, and so on, are <b>not supported whatsoever</b> by LevelledMobs support staff.

<details>
<summary>Why?..</summary>

**The Bukkit API was never written to accommodate mods**, with [all of the hacky methods](https://essentialsx.net/do-not-use-mohist.html) used to try get around this, lots of things get broken in ways which are very difficult for plugin developers to track down. We've come across a handful of server owners with very weird bugs, which were found to be caused by the 'hybrid' server software.

LevelledMobs is not alone in refusing to support hybrid server software. [Even EssentialsX denounces them.](https://essentialsx.net/do-not-use-mohist.html).

</details>

# Java Versions

If you're running `MC v1.17` or `MC v1.16`, you'll need to install Java 17 (or newer) to run LevelledMobs.


> **Note:** LevelledMobs support can't help you with managing your Java installations. There are loads of free online tutorials.

# LevelledMobs Versions

We will **only** support users running the **latest** release or dev build of LevelledMobs.

By running an outdated version you are not only missing out on features, but also various enhancements such as bug fixes and performance upgrades.

<details>
<summary>But I don't want to update LevelledMobs!</summary>

If there is anything that is stopping you from updating, please let us know so we can help you out. Usually, we find these users have invalid or easily resolvable concerns. Reach out to our support staff! :)

</details>

# <u>Incompatible</u> Plugins

<b><u>This does not mean that all of these plugins are <i>fully</i> incompatible... read their descriptions.</u></b>

<table>
    <tr>
        <th width="15%">Plugin</th>
        <th width="15%">Severity</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>mcMMO</td>
        <td>🟢 Low</td>
        <td>
            mcMMO has a health bar function you'll need to disable. It causes visual issues with LM's nametags.
        </td>
    </tr>
    <tr>
        <td>ModelEngine</td>
        <td>🟡 Medium</td>
        <td>
            LevelledMobs' nametag packets are overridden by ModelEngine, so those mobs will be levelled but they won't have a nametag. We can't solve this on our end.
            </br>
            Community members have helped to build a <a href="https://github.com/ArcanePlugins/LevelledMobs/wiki/Compatibility-%7C-LevelledMobs,-ModelEngine,-and-MythicMobs">work-around solution to this issue</a>.
        </td>
    </tr>
    <tr>
        <td>HoloMobHealth <i>(and any other nametag health bar plugins)</i></td>
        <td>🟡 Medium</td>
        <td>
            Just like mcMMO, the health bars cause visual issues with LM's nametags. You'll need to disable the feature or remove that plugin.
            <br />
            You may want to consider using a boss bar or action bar health system instead.
        </td>
    </tr>
    <tr>
        <td>Stacker Plugins</td>
        <td>🔴 Very High</td>
        <td>
            Stackers cause issues with LevelledMobs unless configured: you need to <b>disable mob stacking</b>
            in your stacker plugin as these can break LM's name-tags and custom drop system.
        </td>
    </tr>
    <tr>
        <td>PerWorldPlugins</td>
        <td>🔴 Very High</td>
        <td>
            PerWorldPlugins breaks a *ton* of plugins, including LevelledMobs.
            <br />
            LevelledMobs has per-world functionality via the Rules System, it is entirely pointless to use PerWorldPlugins for LevelledMobs.
            <br />
            You can run PWP and LM together on a server, just do not use PWP to manage the LevelledMobs plugin.
        </td>
    </tr>
</table>

***

# <u>Compatible</u> (and integrated) plugins

### We provide an integration for these plugins:

- `MythicMobs`
- `InfernalMobs`
- `EliteMobs`
- `Shopkeepers`
- `Citizens`
- `DangerousCaves 2`
- `EcoBosses`
- `SimplePets`

Most of these integrations exist so that LevelledMobs, by default, won't make mobs from those plugins become levelled ones.

### Plugins which provide an integration for LM:

- [`MobHunting`](http://www.spigotmc.org/resources/mobhunting.3582/): earn more money from killing higher level mobs
- [`Money From Mobs`](https://www.spigotmc.org/resources/money-from-mobs-1-12-1-17.79137/): earn more money from killing higher level mobs
