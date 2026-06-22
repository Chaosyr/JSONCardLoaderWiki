First as a quick note, this is based on the release system found here: https://github.com/MADH95/JSONLoader/releases

# INSTALLATION

## Setting up the API

### Installing with a Mod Manager
1. Download and install [Thunderstore Mod Manager](https://www.overwolf.com/app/Thunderstore-Thunderstore_Mod_Manager), [Gale](https://thunderstore.io/c/inscryption/p/Kesomannen/GaleModManager/) or [r2modman](https://thunderstore.io/c/inscryption/p/ebkr/r2modman/).
2. Click the **Install with Mod Manager** button on the top of [BepInEx's](https://thunderstore.io/c/inscryption/p/BepInEx/BepInExPack_Inscryption/) page.
3. Run the game via the mod manager.

If you have issues with Mod Managers head to one of these discords;

* **Thunderstore Support Discord:** [Here](https://discord.gg/Fbz54kQAxg)
* **R2ModMan Support Discord:** [Here](https://discord.gg/R85wjqa4WN)
* **Gale Mod Manager Support Discord:** [Here](https://discord.gg/sfuWXRfeTt)

### Installing Manually
1. Install [BepInEx](https://thunderstore.io/package/download/BepInEx/BepInExPack_Inscryption/5.4.1902/) by pressing `Manual Download` and extract the contents into a folder. **Do not extract into the game folder!**
2. Move the contents of the `BepInExPack_Inscryption` folder into the game folder (where the game executable is; usually found here: `C:\Program Files (x86)\Steam\steamapps\common\Inscryption`).
3. Run the game. If everything was done correctly, you will see the BepInEx console appear on your desktop. Close the game after it finishes loading.
4. Install [MonoModLoader](https://inscryption.thunderstore.io/package/BepInEx/MonoMod_Loader_Inscryption/) and extract the contents into a folder.
5. Move the contents of the `patchers` folder into `BepInEx/patchers` (If any of the mentioned BepInEx folders don't exist, just create them).
6. Install [Inscryption API](https://inscryption.thunderstore.io/package/API_dev/API/) and extract the contents into a folder.
7. Move the contents of the `plugins` folder into `BepInEx/plugins` and the contents of the `monomod` folder into the `BepInEx/monomod` folder.
8. Run the game again. If everything runs correctly, a message will appear in the console telling you that the API was loaded.
9. For any additional mods create a new subfolder, it can be called anything and extract the zips archive into it and if there is a `BepInEx` folder within the zip instead drop the contents of that folder into the `BepInEx` root for the modding instance. EX;
    ```
    BepInEx // These go within the BepInEx root folder
    |-- config
    |-- patchers
    |-- plugins
    |-- monomod
    |-- core
    plugins // Files within go into the created plugin subfolder that was created for the mod
    |-- Art
    |-- Scripts
    |-- MyMod.dll
    manifest.json     --|
    README.md           |-- These can be ignored but if you want to keep them put them in the plugin subfolder
    CHANGELOG.md        |--
    icon.png          --|
    ```
10. Run the game once more and everything should be correct and working.

### Installing Manually (XBOX Game-Pass)
1. Install [BepInEx](<https://github.com/BepInEx/BepInEx/releases/tag/v5.4.21>) by pressing `BepInEx_x64_5.4.21.0.zip` and extract the contents into a folder.
2. Move the contents into the game folder (where the game executable is; usually found here: `C:\XboxGames\D30AC640-4EC1-4D15-96F3-384052F09699\Content`).
3. Run the game. If everything was done correctly, you will see the BepInEx console appear on your desktop. Close the game after it finishes loading. (psst. Enable Logging in `BepInEx/config`)
4. Install [MonoModLoader](<https://inscryption.thunderstore.io/package/BepInEx/MonoMod_Loader_Inscryption/>) and extract the contents into a folder.
5. Move the contents of the `patchers` folder into `BepInEx/patchers` (If any of the mentioned BepInEx folders don't exist, just create them).
6. Install [Inscryption API](<https://inscryption.thunderstore.io/package/API_dev/API/>) and extract the contents into a folder.
7. Move the contents of the `plugins` folder into `BepInEx/plugins` and the contents of the `monomod` folder into the `BepInEx/monomod` folder.
8. Run the game again. If everything runs correctly, a message will appear in the console telling you that the API was loaded.
9. For any additional mods create a new subfolder, it can be called anything and extract the zips archive into it and if there is a `BepInEx` folder within the zip instead drop the contents of that folder into the `BepInEx` root for the modding instance. EX;
    ```
    BepInEx // These go within the BepInEx root folder
    |-- config
    |-- patchers
    |-- plugins
    |-- monomod
    |-- core
    plugins // Files within go into the created plugin subfolder that was created for the mod
    |-- Art
    |-- Scripts
    |-- MyMod.dll
    manifest.json     --|
    README.md           |-- These can be ignored but if you want to keep them put them in the plugin subfolder
    CHANGELOG.md        |--
    icon.png          --|
    ```
10. Run the game once more and everything should be correct and working.

### Installing on the Steam Deck
1. Download [r2modman](https://thunderstore.io/c/inscryption/p/ebkr/r2modman/) on the Steam Deck's Desktop Mode and open it from its download using its `AppImage` file.
2. Download the mods you plan on using and their dependencies.
3. Go to the setting of the profile you are using for the mods and click `Browse Profile Folder`.
4. Copy the BepInEx folder, then go to Steam and open Inscryption's Properties menu
5. Go to `Installed Files` click `Browse` to open the folder containing Inscryption's local files; paste the BepInEx folder there.
6. Enter Gaming Mode and check 'Force the use of a specific Steam Play compatibility tool' in the Properties menu under `Compatibility`.
7. Go to the launch parameters and enter `WINEDLLOVERRIDES="winhttp.dll=n,b" %command%`.
8. Open Inscryption. If everything was done correctly, you should see a console appear on your screen.

### Mac & Linux
1. Follow the steps here first: <https://docs.bepinex.dev/articles/user_guide/installation/index.html>
2. Next do steps 4-10 of the Manual Installation
3. Your game should be setup for inscryption modding now

If you have any issues with Mac/Linux, Steam Deck, or Manual head over to the discord for this game:

* **Inscryption Modding Discord:** [Here](https://discord.gg/ZQPvfKEpwM)

## Installing the Package

### Manager
1. Open the Application, Navigate to the Game, Navigate to the Profile.
2. Press `Browse` or the Manager's equivalent
3. Install `MADH95Mods` - `JSONCardLoader`.
4. When you launch JSONLoader is now installed.

### Manual
1. Press `Download`
2. Extract the Zip to a new folder.
3. Take the files and folders under `plugins` of the zip and move them up a folder.
4. Delete the `plugins` folder from the Extracted directory.
5. Now navigate to the location of your BepInEx install from your earlier setup for the API.
6. Navigate to `plugins` and add a folder entitled `MadH95-JSONCardLoader`, if theres a previous version of JSONLoader installed it should be fine, but I'd advise removing it to keep storage down.
7. Move the setup from steps `2-4` into the folder you created in step `7`.
8. Now if all went well you should see the game warn `[Warning:   BepInEx] Plugin [JSONLoader 2.7.0] targets a wrong version of BepInEx (5.4.20.0) and might not work until you update`, this has no relevance to anything and you can safely ignore it, but if the version is `2.7.0` than you have the correct version of JSONLoader installed.