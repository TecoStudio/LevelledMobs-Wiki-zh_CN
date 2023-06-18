```
This page was last updated for LevelledMobs 3.2.4 b557
```

---

# Custom Drops

In his spare time, **UltimaOath** writes special CustomDrops using the Drop-Table system. All of these are written using Vanilla Minecraft mechanics, or 3rd party plugin compatible features such as NBT-API (these will be marked as such). I have also written a short description of the purpose behind the drop-table's creation, though you can use them however you desire!  
  
You can download the full [_UltimaOath Edition_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_oathedition.yml), which includes all of the samples below together.  
 

*   Tiered Tool Sets
    *   [_Netherite Armor and Weapons_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_tiered_netherite_tools.yml)
    *   [_Diamond Armor and Weapons_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_tiered_diamond_tools.yml)
    *   [_Iron Armor and Weapons_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_tiered_iron_tools.yml)
    *   [_Leather Armor and Weapons_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_tiered_wooden_tools.yml)  
          
        These drop tables were designed to be equipped and dropped by entities like skeletons and zombies. Each table contains a single item in varying states of damage, and one of those will be selected for the entity to possibly equip and drop. The item is more likely to appear in a more damaged state, and is less likely to appear in near full durability, though it is still possible.  
        Each of these tiered tool sets include: helmet, chestplate, leggings, boots, axe, sword, and bow/arrow.  
          
         
*   [NBT-API](https://www.spigotmc.org/resources/nbt-api.7939/) Required \\ Special Drop Items
    *   [_Tipped Arrows_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_nbtapi_tippedarrows.yml)
    *   [_Potions_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_nbtapi_potions.yml)
    *   [_Enchanted Books_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_nbtapi_enchantedbooks.yml)  
          
        These drop tables require the plugin NBT-API.  
        They were designed to be dropped by entities upon death as a special drop.  
          
         
*   xEffects Library (Download the [Complete Library](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_xeffects_library.yml) here)
    *   [_Particle Effects_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_xeffects_particles.yml)
    *   [_Sound Effects_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_xeffects_sounds.yml)
    *   [_Area Effects_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_xeffects_aoe.yml)
          
        These drop tables are designed to occur on the death of an entity. These produce various customizable particle, sound, and 'area of effect' effects. They are designed using the native Minecraft commands and should be functional on most server environments.

*   Miscellaneous
    *   [_The Random Stuff_](https://github.com/UltimaOath/LevelledMobs/blob/master/src/main/resources/customdrops_misc.yml)  
          
        These are drop tables that didn't really meet a specific category criteria. These include things like a drop table for the Minecraft discs.

---