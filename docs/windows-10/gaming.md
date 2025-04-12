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
  * [SNES (Super Nintendo)](emulation/snes.md)
  * [N64 (Nintendo 64)](emulation/n64.md)
* SEGA
  * [SMS (SEGA Master System)](emulation/sms.md)
* Sony
  * [PS1 (PlayStation 1)](emulation/ps1.md)
  * [PS2 (PlayStation 2)](emulation/ps2.md)

## Manual configuration

In **Graphics settings** (Windows Settings), browse for the game exe file and choose **High performance**.

Right click on the exe file file and select **Troubleshoot compatibility** (the wizard may select Windows 7 settings for old games).

## Savegames

Game                    | Installer | Save location
------------------------|-----------|--------------------------------------------------------------
Dungeon Siege           | Steam     | `C:\Users\...\Documents\Dungeon Siege`
Max Payne 3             | Steam     | `C:\Users\...\Documents\Rockstar Games\Max Payne 3`
Medal of Honor Airborne | Steam     | `C:\Users\...\Documents\EA Games\Medal of Honor Airborne(tm)`
GTA IV                  | Steam     | `C:\Users\...\Documents\Rockstar Games\GTA IV`

## Patches

### Dungeon Siege

Go to `C:\Program Files (x86)\Steam\steamapps\common\Dungeon Siege 1` and run `DSVideoConfig.exe`.

Then, you can edit `C:\Users\...\Documents\Dungeon Siege\DungeonSiege.ini`, in particular this lines:

```ini
driver_description = Primary Display Driver - Hardware TnL
width = 1600
height = 900
bpp = 32
```

Run the game (exe file is located in `C:\Program Files (x86)\Steam\steamapps\common\Dungeon Siege 1\DungeonSiege.exe`).
