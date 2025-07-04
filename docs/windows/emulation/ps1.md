# Emulation of Sony PlayStation 1 console

## Emulators

### ePSXe

→ [epsxe.com](http://www.epsxe.com/)

### DuckStation

> DuckStation is a simulator/emulator (...), focusing on playability, speed, and long-term maintainability.
> The goal is to be as accurate as possible while maintaining performance suitable for low-end devices.
> "Hack" options are discouraged, the default configuration should support all playable games with only some of the enhancements having compatibility issues.

→ [duckstation.org](https://www.duckstation.org/) ([GitHub](https://github.com/stenzek/duckstation), [Wiki](https://www.duckstation.org/wiki/Main_Page))

#### DuckStation installation

* Download from [GitHub Releases](https://github.com/stenzek/duckstation/releases/tag/latest), unzip the file and go in this directory
* Create `bios` folder and copy bios files inside
* Open `duckstation-qt-x64-ReleaseLTCG.exe` and open Settings (ideas taken from [ETA PRIME video](https://www.youtube.com/watch?v=xdrKCfVohk4))
  * In "BIOS Settings", update bios location
  * In "Controller Settings", change controller type to Analog Controller (DualShock) and map the keys with your controller or load profile (below the mapping)
  * In "Game List Settings", add path to game files (bin/cue)
  * In "Display Settings", enable VSync, specify adapter (if multiple video cards)
  * In "Enhancement Settings", update Internal Resolution Scale to 9x (fir 4K), Texture Filtering to xBR
  * In "General Settings", check Start Fullscreen

Data files are stored in `C:\Users\...\Documents\DuckStation`.

#### DuckStation shortcuts

* Full screen: `Alt`+`Enter` to exit

## Disks

Original disks can be saved as iso files on hard drive disks, with free tools like [BurnAware](https://www.burnaware.com/).
You may have issues with missing SBI files, you can find them at [psxdatacenter.com](http://psxdatacenter.com/sbifiles.html).

## Memory cards

Making a back-up of game saves in memory cards is not intended but there are ways to do it.

One solution is to use a PS2 console with a preinstalled Free Memory Card Boot (see [PS2 emulation](ps2-emulation.md)).

Files copied (with `copy` in uLaunchELF) can then be transferred to a PS1 memory card (mcd) with [memcardrex](https://github.com/ShendoXT/memcardrex).
The save can then be transferred to DuckStation memory file from DuckStation.

## Games

### Best-of

* Boold Omen: Legacy of Kain
* Crash Team racing
* Driver
* Final Fantasy VII
* Final Fantasy VIII
* Rayman 2: The Great Escape
* Soul Blade
* Tomb Raider III
* Vagrant Story
