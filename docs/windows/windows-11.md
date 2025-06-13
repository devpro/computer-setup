# Windows 11

## Configuration

### Power options

Open `Control Panel` > `Hardware and Sound` >  `Power Options` > `Sytem Settings`.

In  `Shut-down settings`, check `Hibernate`.

### Display

Review and update:

Parameter                               | Path
----------------------------------------|----------------------------------------------------------------------------------------------------
HDR                                     | `Settings` (Windows) > `System` > `Display` > `HDR` (in Brightness & Colour)
Windows refresh rate (for every screen) | `Settings` (Windows) > `System` > `Display` > `Advanced display` (Related settings) > `Choose a refresh rate`
NVIDIA G-SYNC                           | `NVIDIA Control Panel` > `Display` > `Set up G-SYNC` > `Enable G-SYNC`
NVIDIA 3D program settings              | `NVIDIA Control Panel` > `3D Settings` > `Manage 3D settings` > `Program settings`
NVIDIA application settings             | `Settings` (Windows) > `System` > `Display` > `Graphics` > `Customised settings for applications`

## Features

### Windows Subsystem for Linux (WSL)

Open a dos window as Administrator to install the default Linux system (Ubuntu 24.04):

```dos
wsl --install
```

Ubuntu is now available in Windows Terminal.

[Install Docker](../ubuntu/ubuntu-24_04.md#docker).

## Applications

### Utilities

* KeePass
  * Plugins: [KeeTheme](https://github.com/xatupal/KeeTheme) (dark theme)
* WinDirStat

    ```dos
    winget install WinDirStat.WinDirStat
    ```
