```
This page was last updated for LevelledMobs 3.8.2
```

***

We use **Maven**.

Starting with LevelledMobs 3.6.0, NMS is now used. This means you'll have to build the remapped version of spigot
being targetting in the source code.<br>
At the time of writing, it is 1.19.
<br>

## Follow these steps to build any remapped version of spigot:
1. Download buildtools.jar from https://hub.spigotmc.org/jenkins/job/BuildTools/
2. Run the following command, substituting the version you want to build: `java -jar BuildTools.jar --rev 1.19.2 --remapped`


## Building LevelledMobs
1. Simply run `mvn clean package`, and you're good to go!

The compiled `.jar` will be processed and become available inside the `/target/` folder, located inside the project you are working in. The `/target/` folder is in the same folder as `/src/`, `pom.xml`, and so on.