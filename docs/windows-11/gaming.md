# Gaming on Windows 11

## Mods

### Vortex Mod Manager

Download the installer from [nexusmods.com](https://www.nexusmods.com/about/vortex) (for example `Vortex-1-1-13-7-1737460629.exe`), then install it.

## Games

### GTA IV CE

Buy the game "Grand Theft Auto IV: The Complete Edition" on Steam and install it.

<!--
Go to [GTA IV: CE – Project Reborn](https://steamcommunity.com/sharedfiles/filedetails/?id=3298411479).
Download the file "GTA IV_ CE – Project Reborn.7z" and unzip it.
Copy the contents to `C:\Program Files (x86)\Steam\steamapps\common\Grand Theft Auto IV\GTAIV` (will overwritte some existing files).
-->

Follow instructions given [ThirteenAG/GTAIV.EFLC.FusionFix](https://github.com/ThirteenAG/GTAIV.EFLC.FusionFix) (download, extract, copy)

Run the game (exe file is located in `C:\Program Files (x86)\Steam\steamapps\common\Grand Theft Auto IV\GTAIV\GTAIV.exe`.

Use auto configure for the graphics settings.

### Mafia III

Buy the game on Steam and install it.

Browse local files (in Manage) from Stream (`C:\Program Files (x86)\Steam\steamapps\common\Mafia III`), open Properties from `Mafia3DefinitiveEdition.exe`.

Check `Disable full-screen optimizations` (and maybe `Run this program as administrator`).

Run the game.

### Max Payne

References: [PCGamingWiki](https://www.pcgamingwiki.com/wiki/Max_Payne)

Install from Steam.

Apply [Max Payne 1, Complete FixPack - 2025 Edition](https://steamcommunity.com/sharedfiles/filedetails/?id=1633394421):

* Download `MP1-Fixpack v1.2025.1.exe`
* Run the exe file
  * Change path to `C:\Program Files (x86)\Steam\steamapps\common\Max Payne`
  * Set D11

Open properties of `C:\Program Files (x86)\Steam\steamapps\common\Max Payne\MaxPayne.exe`:

* In `Compatibility` tab: check `Disable full-screen optimisations`

Run the game from Steam, chose High in the configuration

### Max Payne 2

References: [PCGamingWiki](https://www.pcgamingwiki.com/wiki/Max_Payne_2:_The_Fall_of_Max_Payne)

Install from Steam.

Download `MaxPayne2.WidescreenFix.zip` from [ThirteenAG/WidescreenFixesPack](https://github.com/ThirteenAG/WidescreenFixesPack/releases/tag/mp2), extract the files in `C:\Program Files (x86)\Steam\steamapps\common\Max Payne 2 The Fall of Max Payne`.

Run the game, select `2560 x 1440 x 32` in **Screen Mode**, and **Reset All Settings** to `High` in Options.

Seems to add an improvement, in **NVIDIA Control Panel** application, in **3D Settings**, **Manage 3D Settings**, select `Max Payne 2 (maxpayne2.exe)` in **Program Settings** and change:

* **Monitor Technology**: `Fixed Refresh`
* **Anisotropic filtering**: `Off`

### Skyrim SE (Special Edition)

Browse the available mods from [Nexus Mods](https://www.nexusmods.com/games/skyrimspecialedition).

Install the mods (click on the Vortex link after Download on top right):

* [Skyrim Script Extender (SKSE64)](https://www.nexusmods.com/skyrimspecialedition/mods/30379?tab=description)
* [Unofficial Skyrim Special Edition Patch - USSEP](https://www.nexusmods.com/skyrimspecialedition/mods/266)
* [SkyUI](https://www.nexusmods.com/skyrimspecialedition/mods/12604)
* [Address Library for SKSE Plugins](https://www.nexusmods.com/skyrimspecialedition/mods/32444)
* [Static Mesh Improvement Mod - SMIM](https://www.nexusmods.com/skyrimspecialedition/mods/659)

Run the game from Vortex.
