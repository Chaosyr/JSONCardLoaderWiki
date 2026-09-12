### JSON Inscrybing
All JSONLoader versions require the same things so, heres a unified basics for making things with JSONLoader. First off make sure you have a Keyboard, Mouse, Monitor, File Explorer, and a Text Editor. These are more or less all you need to make JSON's for this mod. However there are some mandatory steps to get your environments prepared.

#### File Explorer (Windows)
In order for you to make the actual JLDR extension for your cards you'll need to follow the below steps in your File Explorer.
1. Open File Explorer
2. Find the `…` (or 3 dots in a row) button, and press it.
3. Press `[Insert a Wrench Here] Options`.
4. In the menu that just popped up you'll see 3 Tabs at the top, press the one labeled `View`.
5. Under `Advanced Settings:` toggle off `Hide extensions for known file types`, another useful one to toggle would be `Show hidden files, folders, and drives`.
6. After you've toggled these press `Apply to Folders`.
7. Next, press `OK`.

Now you should see File Extensions alongside all of your files. As stated before this will allow you to change the File Extension for the mod. 

#### Getting the Path's
Next up you'll likely want to grab a path, namely the one to your Plugins folder. This folder will lie wherever your BepInEx folder is. 

If you use a Mod Manager, go to one of the following places:
* R2ModMan: `Settings` -> `Directories` -> `Profile Folder` -> `Browse` -> Navigate via File Explorer to `BepInEx` -> Navigate via File Explorer to `plugins` -> Go to the File Explorer Address Bar -> Click It -> Hit `CTRL+C` or the OS Equivalent. 
* GaleModManager: Click `File` in the Top Bar -> `Browse Profile Folder` -> Navigate via File Explorer to `BepInEx` -> Navigate via File Explorer to `plugins` -> Go to the File Explorer Address Bar -> Click It -> Hit `CTRL+C` or the OS Equivalent.
* ThunderstoreModManager: `Settings` -> `Directories` -> `Profile Folder` -> `Browse` -> Navigate via File Explorer to `BepInEx` -> Navigate via File Explorer to `plugins` -> Go to the File Explorer Address Bar -> Click It -> Hit `CTRL+C` or the OS Equivalent.

If your manual it should be something like:
1. Navigate to the Games Local Install Folder
  * XboxGames: `C:\XboxGames\Inscryption\Content`
  * Steam: `\steamapps\common\Inscryption` after you get to the Steam Install Folder. 
2. Next navigate to `BepInEx/plugins`
3. Go to the File Explorer Address Bar -> Click It -> Hit `CTRL+C` or the OS Equivalent.

Now store that path somewhere you'll remember it, you'll be coming back here a lot over the course of your mod.

#### Text Editor
The recommended File Editor for JSONLoader is [VisualStudioCode](https://code.visualstudio.com/) as it has built in handlers for both JSON Syntax and CSV Syntax, if your working with JSONLoader at any point this should be your go-to editor, but if you have a preficed editor nothings stopping you from using it. If you don't want to download anything there is a Website called [JSONEditorOnline](https://jsoneditoronline.org/) which does similar.

#### Adding the File Extensions to the Context Menu (Windows 11)
I'm going to include this for those on Windows 11 for other OS's the next section should work fine.

1. In A Text Editor Create a new File.
2. Enter the following into the file:
   ```ini
   Windows Registry Editor Version 5.00

   [HKEY_CLASSES_ROOT\.md]
   @="markdownfile"
   
   [HKEY_CLASSES_ROOT\.md\ShellNew]
   "NullFile"=""
   
   [HKEY_CLASSES_ROOT\markdownfile]
   @="Markdown Document"
   
   [HKEY_CLASSES_ROOT\markdownfile\DefaultIcon]
   @="\"C:\\Users\\Chaos\\AppData\\Local\\Programs\\Microsoft VS Code\\a44adf7f53\\resources\\app\\resources\\win32\\markdown.ico\""
   
   [HKEY_CLASSES_ROOT\.json]
   @="jsonfile"
   
   [HKEY_CLASSES_ROOT\.json\ShellNew]
   "NullFile"=""
   
   [HKEY_CLASSES_ROOT\jsonfile]
   @="JSON File"
   
   [HKEY_CLASSES_ROOT\jsonfile\DefaultIcon]
   @="\"C:\\Users\\Chaos\\AppData\\Local\\Programs\\Microsoft VS Code\\a44adf7f53\\resources\\app\\resources\\win32\\json.ico\""
   
   [HKEY_CLASSES_ROOT\.jldr]
   @="jldrfile"
   
   [HKEY_CLASSES_ROOT\.jldr\ShellNew]
   "NullFile"=""
   
   [HKEY_CLASSES_ROOT\jldrfile]
   @="JSONLoader File"
   
   [HKEY_CLASSES_ROOT\jldrfile\DefaultIcon]
   @="\"C:\\Users\\Chaos\\AppData\\Local\\Programs\\Microsoft VS Code\\a44adf7f53\\resources\\app\\resources\\win32\\json.ico\""
   
   [HKEY_CLASSES_ROOT\.jldr2]
   @="jldr2file"
   
   [HKEY_CLASSES_ROOT\.jldr2\ShellNew]
   "NullFile"=""
   
   [HKEY_CLASSES_ROOT\jldr2file]
   @="JSONLoader2 File"
   
   [HKEY_CLASSES_ROOT\jldr2file\DefaultIcon]
   @="\"C:\\Users\\Chaos\\AppData\\Local\\Programs\\Microsoft VS Code\\a44adf7f53\\resources\\app\\resources\\win32\\json.ico\""
   
   [HKEY_CLASSES_ROOT\.jldr3]
   @="jldr3file"
   
   [HKEY_CLASSES_ROOT\.jldr3\ShellNew]
   "NullFile"=""
   
   [HKEY_CLASSES_ROOT\jldr3file]
   @="JSONLoader3 File"
   
   [HKEY_CLASSES_ROOT\jldr3file\DefaultIcon]
   @="\"C:\\Users\\Chaos\\AppData\\Local\\Programs\\Microsoft VS Code\\a44adf7f53\\resources\\app\\resources\\win32\\json.ico\""
   
   [HKEY_CLASSES_ROOT\.csv]
   @="csvfile"
   
   [HKEY_CLASSES_ROOT\.csv\ShellNew]
   "NullFile"=""
   
   [HKEY_CLASSES_ROOT\csvfile]
   @="CSV File"
   
   [HKEY_CLASSES_ROOT\csvfile\DefaultIcon]
   @="\"C:\\Users\\Chaos\\AppData\\Local\\Programs\\Microsoft VS Code\\a44adf7f53\\resources\\app\\resources\\win32\\html.ico\""
   ```
3. Save the file as a `[SomeName].reg`, then run it.
4. Next Restart your File Explorer via Task Manager

What this did was add the following file types to your Right Click Context Menu: `.md`, `.json`, `.jldr`, `.jldr2`, `.jldr3`, and `.csv`. So that now when you want to make a new JSONLoader file you can press `New` -> `JSONLoader(X) File` in the Context Menu. Note for the Icons this is set to utilize those of [Visual Studio Code](https://code.visualstudio.com/)

#### Creating the JSON File

Now you'll need to make the actual file for your Item added by JSONLoader. Go to the Plugins folder, then you'll make a new directory or folder under it, this will be your Mod's folder. Make another directory under it called simply `plugins` this will make your life a little easier when uploading your mods, as the folders will be sticky. Now make a folder called `Scripts`, this will be where your JSON's are expected to live unless you explicitly define it in a file included in your mod, that's not relevant now though.

Once that's done, Right-Click the window explorer pane in the folder, Select New `Text Document` or New `JSONLoader(X) File`, ensure the extension of the file matches the Item your trying to create. Now Open the file in a Text Editor, and insert `{}` into the file, this is so you have a valid JSON base. Each Support area of the Documentation will cover what to put into this file.

Oh, before I leave you, give this a watch: [Web Dev Simplified: Learn JSON in 10 Minutes](https://www.youtube.com/watch?v=iiADhChRriM), this will give you a overview of what JSON is and how to work with it, and it will teach you the terminology.