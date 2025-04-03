# Gaming on Windows 10

## Applications

* Epic Games
* [GOG GALAXY](https://www.gogalaxy.com/)
* [NVIDIA GeForce NOW](https://www.nvidia.com/en-us/geforce-now/download/)
* Steam
* Ubisoft Connect

## Console emulation

* [Amiga](emulation/amiga.md)
* Nintendo
  * [Super Nintendo](emulation/snes.md)
  * [Nintendo 64](emulation/n64.md)
* Sega
  * [SEGA Master System](emulation/sms.md)
* Sony
  * [Sony PlayStation 1](emulation/ps1.md)
  * [Sony PlayStation 2](emulation/ps2.md)

## Configuration

In **Graphics settings** (Windows Settings), browse for the game exe file and choose **High performance**.

Right click on the exe file file and select **Troubleshoot compatibility*** (the wizard may select Windows 7 settings for old games).

## Savegames

Game                    | Installer | Save location
------------------------|-----------|--------------------------------------------------------------
Dungeon Siege           | Steam     | `C:\Users\...\Documents\Dungeon Siege`
Max Payne 3             | Steam     | `C:\Users\...\Documents\Rockstar Games\Max Payne 3`
Medal of Honor Airborne | Steam     | `C:\Users\...\Documents\EA Games\Medal of Honor Airborne(tm)`
GTA IV                  | Steam     | `C:\Users\...\Documents\Rockstar Games\GTA IV`

## Games

### Dungeon Siege

Exe file: `C:\Program Files (x86)\Steam\steamapps\common\Dungeon Siege 1\DungeonSiege.exe`

In **File Explorer**, go to `C:\Program Files (x86)\Steam\steamapps\common\Dungeon Siege 1` and run `DSVideoConfig.exe`. Then, you can edit `C:\Users\...\Documents\Dungeon Siege\DungeonSiege.ini`, in particular this lines:

```ini
driver_description = Primary Display Driver - Hardware TnL
width = 1600
height = 900
bpp = 32
```

### GTA IV

Exe file: `C:\Program Files (x86)\Steam\steamapps\common\Grand Theft Auto IV\GTAIV\GTAIV.exe`

Buy the game on Steam "Grand Theft Auto IV: The Complete Edition".

Go to [GTA IV: CE – Project Reborn](https://steamcommunity.com/sharedfiles/filedetails/?id=3298411479), download the file "GTA IV_ CE – Project Reborn.7z", unzip it and copy the contents to `C:\Program Files (x86)\Steam\steamapps\common\Grand Theft Auto IV\GTAIV` (will overwritte some existing files).
