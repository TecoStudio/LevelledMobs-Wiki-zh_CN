```
This page was last updated for LevelledMobs 3.1.0 b475
```

***

# Maven Dependency
Add the JitPack repository.
```xml
<repository>
    <id>jitpack.io</id>
    <url>https://jitpack.io</url>
</repository>
```

Add the LevelledMobs dependency.
```xml
<dependency>
    <groupId>com.github.lokka30</groupId>
    <artifactId>LevelledMobs</artifactId>
    <version>REPLACE ME</version>
</dependency>
```
Replace `REPLACE ME` with the latest version (not including build number!) of LevelledMobs, e.g. `3.1.0`.

# Accessing LevelledMobs directly
We offer the [LevelInterface](https://github.com/lokka30/LevelledMobs/blob/master/src/main/java/me/lokka30/levelledmobs/LevelInterface.java) class to interact directly with LevelledMobs.

# Events
We also offer a bunch of [events](https://github.com/lokka30/LevelledMobs/tree/master/src/main/java/me/lokka30/levelledmobs/events) which you can listen to and modify.

You can prevent mobs from being levelled, run stuff after they have been levelled, and so on.

# Javadocs
You may view the [javadocs](https://lokka30.github.io/LevelledMobs/) we have compiled so far.

These show our code documentation which we are gradually improving.

# Integrating Into Custom Drops

If you want to integrate your plugin directly into LM's custom drop system, we have an API for it.
Sample code is below.

```java
    private void testCustomDrops(){
        ItemStack itemStack = new ItemStack(Material.NETHERITE_SWORD);
        ItemMeta meta = itemStack.getItemMeta();
        assert meta != null;
        meta.setDisplayName("Cool Netherite Sword");
        meta.setLore(List.of("Created via API"));
        itemStack.setItemMeta(meta);

        // https://arcaneplugins.github.io/LevelledMobs/3.9.3/me/lokka30/levelledmobs/LevelledMobs.html
        LevelledMobs lm = LevelledMobs.getInstance();

        // https://arcaneplugins.github.io/LevelledMobs/3.9.3/me/lokka30/levelledmobs/customdrops/CustomDropItem.html
        CustomDropItem customDropItem = new CustomDropItem(lm); // must pass instance to LevelledMobs main class
        customDropItem.setItemStack(itemStack);

        // these options correspond to many of the item specific options shown here:
        // https://github.com/ArcanePlugins/LevelledMobs/wiki/Documentation---customdrops.yml
        customDropItem.chance = 1.0F;
        customDropItem.equippedSpawnChance = 1.0F;

        // https://arcaneplugins.github.io/LevelledMobs/3.9.3/me/lokka30/levelledmobs/customdrops/CustomDropInstance.html
        final CustomDropInstance customDropInstance = new CustomDropInstance(EntityType.ZOMBIE);
        customDropInstance.customItems.add(customDropItem);
        // mob specific options can be set on customDropInstance

        lm.customDropsHandler.externalCustomDrops.addCustomDrop(customDropInstance);
        // the drop is now registered just as if it were in customdrops.yml

        main.getLogger().info("Added a new drop for zombie");
    }
```

***

If you need assistance in using LevelledMobs with your plugin, please contact us! :)