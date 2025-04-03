# Sony PlayStation 2 (PS2) emulation

## Emulators

### PCSX2

> An Open-Source Playstation 2 Emulator supporting over 98% of the original PS2 library

→ [pcsx2.net](https://pcsx2.net/) ([GitHub](https://github.com/PCSX2))

#### PCSX2 quickstart

* Download and install from a [nightly build](https://pcsx2.net/downloads/#nightly-anchor)
  * AVX2 or SSE4 depend on your CPU
* Copy bios file
* Configure controller
* Configure rendering

#### PCSX2 help

* [How Play PS2 Games In 4K On PC - PCSX2 Set Up Guide](https://www.youtube.com/watch?v=3rSiK2aO_5k)

#### PCSX2 shortcuts

* [States](https://wiki.pcsx2.net/Savestate): `F1` to save, `F3` to load

## Disks

Original disks can be saved as iso files on hard drive disks, with free tools like [BurnAware](https://www.burnaware.com/).

## Memory cards

Making a back-up of game saves in memory cards is not intended but there are ways to do it.

One solution is to use a preinstalled Free Memory Card Boot (FMCB), available to buy online, that contain several tools like uLaunchELF ([How to Transfer PS2 Save Game Files from Memory Card To USB Using Free McBoot 2021](https://www.youtube.com/watch?v=vWy_QBeRA-g)).
Additional information from: [FreeMcBoot installers](https://israpps.github.io/FreeMcBoot-Installer/) ([GitHub](https://github.com/israpps/FreeMcBoot-Installer)).
You'll only need a FAT32 USB drive (no format needed, just used to copy/paste).

Files copied with pcuCopy can then be transferred to a PCSX2 memory card with [mymc](http://www.csclub.uwaterloo.ca:11068/mymc/) (solution found from [How to import PS2 Save Files for PCSX2 and AetherSX2 Emulators](https://www.youtube.com/watch?v=70YyoqXBy5A)).

## Games

Name                                  | Supported | Fix?
--------------------------------------|-----------|-----
Burnout 2: Point of impact            | Yes       |
Crash Nitro Kart                      | Yes       |
God of War                            | Yes       |
Godfather, The                        | Yes       | Right click on the game in game list, Properties, Graphics, Rendering (check Manual Hardware Renderer Fixes), Hardware Fixes (Skipdraw Range: 1, 1) ([wiki.pcsx2.net](https://wiki.pcsx2.net/The_Godfather))
Pro Evolution Soccer 6                | Yes       |
The Lord of the Rings: The Two Towers | Yes       |
Theme Park World                      | Yes       |
