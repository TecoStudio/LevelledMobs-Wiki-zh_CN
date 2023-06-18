```
This page was last updated for LevelledMobs 3.1.1 b481
```

***

We would *highly* appreciate if contributors followed this guide, as it will save the lead developers a lot of time having to clean up PRs.

***

# Musts:
* **Before** working on a PR, please contact the development team to make sure it is worthy of your time. If an issue on the issue tracker has the label `contributions welcome` then it is likely we will give you the 👍🏻.
* Please use curly brackets, *especially* if it is an 'if abc else xyz' statement. The only exception is for small 'if' statements, such as `if(enabled) runMethod();`.
* Include javadocs and comments to your code wherever possible, unless it is obviously self-explanatory (e.g. 'changeWoolColor(Block)`)
* Please do not commit any personal IDE settings change unless you feel they are a significant improvement. If you find your IDE is adding its own files then consider adding them to `.gitignore`.
* Do not use automatic code re-arranging from your IDE. We've purposely laid out methods and variables in certain areas, and functions such as IntelliJ's 'relocate code' mess with it.

# Language:
* Wherever possible, use American English (`en-us`) spelling
* The only exception is with the plugin's name, `LevelledMobs`, which was spelt
originally with Australian English (`en-au`) and shall continue to be, to prevent breaking any resources which depend on
this spelling.
  * American English uses `leveled` (two total `l` characters), compared to Australian English's `levelled` (
three total `l` characters).
  * Sorry for this confusion!

# Ownership of Code
* Any contributions must fall under the same license described in `LICENSE.md`.
* You are expected to own or clearly credit the code you have contributed.
  * Check the license of copied code beforehand.