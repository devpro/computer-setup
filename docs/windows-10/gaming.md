# Gaming on Windows 10

## Applications

* [NVIDIA GeForce NOW](https://www.nvidia.com/en-us/geforce-now/download/)
* Epic Games
* Steam
* Ubisoft Connect

## Console emulation

* [Amiga](emulation/amiga.md)
* Nintendo
  * [Nintendo 64](emulation/n64.md)
  * [Super Nintendo](emulation/snes.md)
* Sega
  * [SEGA Master System](emulation/sms.md)
* Sony
  * [Sony PlayStation 1](emulation/ps1.md)
  * [Sony PlayStation 2](emulation/ps2.md)

## Configuration

## Dungeon Siege

In **Graphics settings** (Windows Settings), browse `C:\Program Files (x86)\Steam\steamapps\common\Dungeon Siege 1\DungeonSiege.exe` and choose **High performance**.

In **File Explorer**, go to `C:\Program Files (x86)\Steam\steamapps\common\Dungeon Siege 1` and run `DSVideoConfig.exe`. Then, you can edit `C:\Users\...\Documents\Dungeon Siege\DungeonSiege.ini`, in particular this lines:

```ini
driver_description = Primary Display Driver - Hardware TnL
width = 1600
height = 900
bpp = 32
```

Not needed/not working: "File Explorer", right click on the `DungeonSiege.exe` file and select **Troubleshoot compatibility*** (the wizard will select Windows 7 settings) | In Steam, add the launch options `nointro=true` (`width=1920 height=1080` makes the game crash).

## Retro games

* [/r/Roms Megathread](https://r-roms.github.io/)
