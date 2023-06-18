**This <ins>does not</ins> provide true 1:1 compatibility between the three plugins; this page provides a work-around solution developed by a generous discord community member *tony0099#8012*, who has offered to share their methodology.**

**The primary incompatibility centers around the lack of a displayed nametag on the ModelEngine entities, even if LevelledMobs has levelled the entity. This is due to an override in ModelEngine, and not something we have the ability to fix. This method adds a nametag component to the model itself, which is then recreated in the configuration of MythicMobs for that entity.**

**There will be <ins>ZERO SUPPORT PROVIDED</ins> to implement this modification on your server; We do not have true compatibility between LevelledMobs and ModelEngine. Nor can we guarentee that this method will work for all future versions of any of the involved plugins.**



---

### **Required Plugins/Software:**

* Latest [LevelledMobs](https://www.spigotmc.org/resources/levelledmobs.74304/) plugin; (v3.9.3 used in examples)
* Latest [ModelEngine](https://www.spigotmc.org/resources/conxeptworks-model-engine%E2%80%94ultimate-custom-entity-model-manager-1-16-5-1-19-3.79477/) plugin (v3.1.4 used in examples);
* Latest [MythicMobs](https://www.spigotmc.org/resources/%E2%9A%94-mythicmobs-free-version-%E2%96%BAthe-1-custom-mob-creator%E2%97%84.5702/) plugin (v5.2.0 used in examples);
* [BlockBench](https://www.blockbench.net/) (either the online editor or the program)
* A ModelEngine Model (we use the freely available [Rock Golem](https://mcmodels.net/model/rock-golem/))



---

### **Confirmed issues:**

* Player Levelling does not update the nametag correctly, so should not be used with this work-around.



---

### Step One: Installation and Setup

The first step is to make sure you have all three of the above mentioned plugins installed on your server successfully without errors during startup in console. This step is often overlooked and will result in frusturation and anger later if you do not double check!



---

### Step Two: BlockBench (Part 1)

With everything functioning as it should, open your BlockBench model inside the BlockBench program. You should see something similar to this:

![](https://i.ibb.co/30jFmXn/image.png)



You want to click on the button labeled&nbsp;**Add Group:**

<img src="https://i.ibb.co/587J41g/image.png" width="50%" alt="" />



This will create a new `bone` object, which we need to rename to `tag_nametag`.

<table border="0" style="border-collapse: collapse; width: 100%;">
<tbody>
<tr>
<td style="width: 50%;"><img src="https://i.ibb.co/SPKhnQd/image.png" alt="" /></td>
<td style="width: 50%;"><img src="https://i.ibb.co/1GxPHnp/image.png" alt="" /></td>
</tr>
</tbody>
</table>



---

### Step Three: BlockBench (Part 2)

Now we need to move the new `bone` object called `tag_nametag` to where we want the actual nametag for this entity to display. The numbers you use will be different depending on the model of your entity and where you want to place them. I have placed the nametag above the entity model and slightly forward from the center so it does not clip into the arm.

I suggest if you are not familiar with how to use a 3D editor that you simply change the values of the **Pivot Point** until you are satisfied that the centerpoint of the `bone` object is the centerpoint of where you want your nametag to display.

<img src="https://i.ibb.co/HhwTc3N/image.png" width="50%" alt="" />

<table border="0" style="border-collapse: collapse; width: 100%;">
<tbody>
<tr>
<td style="width: 50%;"><strong>Original Position</strong></td>
<td style="width: 50%;"><strong>New Position</strong></td>
</tr>
<tr>
<td style="width: 50%;"><img src="https://i.ibb.co/2PqdWRx/image.png" alt="" /></td>
<td style="width: 50%;"><img src="https://i.ibb.co/Y8pJshB/image.png" alt="" /></td>
</tr>
</tbody>
</table>



With the `tag_nametag` object representing the nametag in the correct place for your model, you need to ensure you save the changes to the model and place it inside of your **blueprints** folder within the **ModelEngine** plugin folder on your server.

From the console of your server, make sure to perform `/meg reload models` so that a new **Resource Pack** is generated. This pack is how **ModelEngine** applies the custom textures, and is a standard part of using this plugin. For how to apply the resource pack, refer to the **ModelEngine** wiki.



---

### Step Four: LevelledMobs

Now we need to establish how we are going to level this entity. In order to isolate it, we will create a custom rule within **LevelledMobs** which will check for the **MythicMobs** plugin and then the specific named entity. Then it will apply the default `average_challenge` preset to the entity (this sets the `max-health:` multiplier to `5.0`, and the `maxLevel:` to `25`. You do not have to use these settings). For the purposes of the example:

```yml
  - enabled: true
    name: 'MythicMob + ModelEngine | Rocky Golem'
    use-preset: average_challenge
    conditions:
      level-plugins:
        MYTHIC_MOBS: true
      mythicmobs-internal-names: ['ROCKY']
```



---

### Step Five: MythicMobs

With the model ready to go, we need to create various `Skills` and `Variables` within&nbsp;**MythicMobs** which correspond to the attribute changes made within&nbsp;**LevelledMobs** and the application of a faux LevelledMobs nametag.

In order to populate the nametag with the level assigned by **LevelledMobs**, we need to extrapolate that number by what information&nbsp;**MythicMobs** has access to. For that, we use the vanilla health value of the entity and the health it has when it spawns, then reverse engineer&nbsp;**LevelledMobs**'s multiplier formula to determine the level to display.

For example, the formula used to calcuate the final applied health to a levelled entity is as follows (simplified):

<table border="0" style="border-collapse: collapse; width: 100%;">
<tbody>
<tr>
<td style="width: 50%;">
`X = The entity's current level`<br />`D = The LM Max Level value`<br />`A = The current health of the entity at spawn`<br />`B = The vanilla health of the entity at spawn`<br />`C = The LM Multipler config value`</td>
<td style="width: 50%;">
The default Multiplier formula:<br />`A = B + ((B * C) * (X / D))`<br /><br />When we isolate for the entity level:<br />`X = D * (A - B) / (B * C)`
</td>
</tr>
</tbody>
</table>



Inside of the **MythicMobs** plugin folder is the **/Skills/** folder, where you would place the skills file for the **ModelEngine** entity. Inside this skill file you need to create a new unique skill called `LMNametag-Rocky` and populate it with the following information:

---

```yml
LMNametag-Rocky:
  Conditions:
  - playerwithin{d=10} true
  Skills:
  - skill{s=[
    - setvar{var=caster.basehp;type=INTEGER;val="(20)"}
    - setvar{var=caster.lm-max-level;type=INTEGER;val="(25)"}
    - setvar{var=caster.lm-hp-multiplier;type=INTEGER;val="(5)"}
    - setvar{var=caster.lm-hp-max;type=INTEGER;val="(<caster.var.basehp>*<caster.var.lm-hp-multiplier>)"}
    - setvar{var=caster.lm-level;type=INTEGER;val="(((<caster.mhp>-<caster.var.basehp>)*<caster.var.lm-max-level>)/<caster.var.lm-hp-max>)"} 
    - setmodeltag{mid=rocky;bone=nametag;tag=&fLvl. &b<caster.var.lm-level> &f| <caster.display> &f| &f<caster.hp>/<caster.mhp>;v=true} @self
    ]}
```



---

You want to make adjustments to the listed `setvar` based on the values in your **LevelledMobs** config and the default health of the entity listed in **MythicMobs**. 

The first line, `caster.basehp`, represents the `Health: X` config line in your entities **/Mobs/** file. The value used here is `20`, taken from my entities' file.

The second line, `caster.lm-max-level`, represents the `maxLevel:` that this particular entity can receive, taken from the `rules.yml` file configuration for that entity; we used the `average_challenge` preset, which has `maxLevel: 25` by default.

The third line, `caster.lm-hp-multiplier`, represents the `multiplier: max-health:` being applied to the entity, taken from the `rules.yml` file configuration for that entity; we used the `average_challenge` preset, which has `max-health: 5.0` by default.

The fourth and fifth line, `caster.hp-max` and `caster.lm-lvl`, is used to populate a variable for future math and should be ignored.



![](https://i.ibb.co/DbLj8j7/image.png)

You need to take particular note of the sixth line of the above code:<br />`- setmodeltag{mid=rocky;bone=nametag;tag=&fLvl. &b<caster.var.lm-level> &f| <caster.display> &f| &f<caster.hp>/<caster.mhp>;v=true} @self`&nbsp;

There is a section at the front labeled `mid=rocky` which represents the name of the **ModelEngine** model file. You want to change this to reflect the name of the model file you're editing.

You also could adjust anything within `tag=&fLvl. &b<caster.var.lm-level> &f| <caster.display> &f| &f<caster.hp>/<caster.mhp>` to change what is displayed as the nametag format wise. This format returns the following as an example: `Lvl. 1 | Rocky the Golem | 20/20` .



---

With the `Skills` and `Variables` set, we need to include this new skill in the&nbsp;**MythicMobs**&nbsp;**/Mobs/** file so that the&nbsp;**ModelEngine** entity can 'use' the nametag ability.&nbsp;

Add the following line under the `Skills:` tree:<br />`- skill{s=LMNametag-Rocky}`

![](https://i.ibb.co/BKPJGYZ/image.png)



---

### Step Six: Save Changes, Restart Server, and Test!

If everything has configured properly, you should expect to see no errors in your console at startup.

A few notes: These nametags DO NOT WORK like LevelledMobs nametags, and will not respect any setting from LevelledMobs in this regard. We have recreated a fake nametag, and do not have any syncing ability between the two.

These nametags are only displayed once an entity has become hostile to players.

![](https://i.ibb.co/4WPFGPW/image.png)