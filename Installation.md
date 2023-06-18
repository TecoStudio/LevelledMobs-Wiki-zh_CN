```
This page was last updated for LevelledMobs 3.8.2 b720
```

***

# ⚠️ Read before you install LevelledMobs ⚠️ 

**Make sure your server is [compatible](https://github.com/lokka30/LevelledMobs/wiki/Compatibilities).** We have explained compatibility for Minecraft versions, Java versions, server software, plugins, and so on - read the [Compatibilities](https://github.com/lokka30/LevelledMobs/wiki/Compatibilities) Wiki page, *before* you install LevelledMobs.

<details>
<summary>Summary for lazy server owners. 😛</summary>

> Make sure you have...
>
> - `Minecraft 1.16` or newer
> - `Java 17` or newer
> - Servers older than MC 1.19 require [`ProtocolLib`](https://www.spigotmc.org/resources/protocollib.1997/) to be installed as well, except for Paper 1.18.

</details>

***

# 📖 Installation Instructions

Here's how to install LevelledMobs! 😁

These instructions are akin to most other plugins - remember to download any dependencies.

- Download [`LevelledMobs`](https://www.spigotmc.org/resources/levelledmobs.74304/).
- If your server is older than MC 1.19, then download [`ProtocolLib`](https://www.spigotmc.org/resources/protocollib.1997/) in addition to LevelledMobs. Paper servers that are 1.18 or newer do not need ProtocolLib.
- Copy the downloaded file(s) into your server's `plugins/` directory.
- If your server is running, shut it down using the `/stop` command.
- Start your server. This allows LevelledMobs to generate its default configuration files.
  - Feel free to edit these configuration files in the `plugins/LevelledMobs/` directory to your liking.
  - If you make any edits, save the file(s) and run `/lm reload` (or restart your server) to apply the changes.
- All done! We hope you enjoy LevelledMobs! :)

***

# 🧩 Optional Dependencies

The following plugins can be installed at your choice to improve LevelledMobs' functionality. Ensure you get the correct plugin version for your Minecraft version, as the latest versions of some of these plugins don't work with older versions.

- [ProtocolLib](https://www.spigotmc.org/resources/protocollib.1997/) is used to allow 1.16, 1.17, and specifically non-Paper-based 1.18 servers to access packet management code to display labels on mob heads.
- [WorldGuard](https://dev.bukkit.org/projects/worldguard/) allows you to restrict if levelled mobs can spawn in defined regions of your worlds, and optionally what min/max level they are allowed to have there. Perfect for creating dungeons or special zones in your worlds!
- [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) will allow you to use LM placeholders in other PAPI-enabled plugins and will also allow you to use PAPI-enabled plugins in LevelledMobs 3.1+'s player-levelling system.
- [NBT API](https://www.spigotmc.org/resources/nbt-api.7939/) will allow you to specify NBT data in the custom drops system.

***

# ⬆️ Updating LevelledMobs

## 🔎 How do I check for updates?

LevelledMobs usually updates around a week or two after the previous update. However, as LevelledMobs 3 has become a mature plugin, updates may take a month simply as there is no need to release any sooner.

We recommend checking the Spigot page at least once a week for any updates and announcements, unless you have a Spigot account which is 'watching' the resource (it's a link below the download button; it is enabled automatically when you download any plugin).

If you do not update LevelledMobs, then as with all software, you will miss out on new features, improvements and bug fixes. In addition, no support is provided to users who choose to use an outdated version. If you have any concerns about updating, please contact our support staff and we will listen to your concerns and advise you accordingly.

## 📖 How do I update LevelledMobs?

> ### Notice: *Before* you update!
> **Read most of the changelog.** Non-patch updates will almost certainly have important information that you need to understand prior to downloading and installing the updated version. 

> ### Notice: Automatic config migration
> Unless clearly clarified in the changelog of a particular version, LevelledMobs will automatically make any edits to your configuration to ensure it works with the updated version. Regardless, we rarely make changes to the configuration.

Updating LevelledMobs is identical to updating any other plugin on the platform. Remove the old version, pop in the new, restart. 😉

- Download the latest version of [`LevelledMobs`](https://www.spigotmc.org/resources/levelledmobs.74304/).
- If your server is running, shut it down using the `/stop` command.
- Delete the existing `.jar` file for LevelledMobs in your server's `plugins/` directory.
  - This file is named in a similar format to `LevelledMobs-3.4.1_b625.jar`, **ending with `.jar`**.
  - Do not delete the `plugins/LevelledMobs/` directory, unless you want to reset your configuration entirely.
- Copy the downloaded file(s) into your server's `plugins/` directory.
- Start your server.
- You have now updated LevelledMobs! :)