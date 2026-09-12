### Logging
Our API has a unique form of Logging to it you can call `JSONLoader3.FormatLogger()` to access it. 

If you hover over the function it will tell you what the inputs are and what it does. 

This is how we have the fancier color coded logging that BepInEx does not have.

This Logging system is built on top of Cecil.ANSI_Utils from the [Cecil Libraries Organization](https://stoatgames.icu/subsidiaries/cecil-libraries-organization/#header-container-subsite) and ANSI Mod from Stoat Games enables the ability for Windows users.