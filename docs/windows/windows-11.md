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

Make sure systemd is enabled:

```bash
cat /etc/wsl.conf
stat /sbin/init
```

[Install Docker](../ubuntu/ubuntu-24_04.md#docker).

To restrict the use of resources by WSL2 (all distros), create a text file `%UserProfile%\.wslconfig` in the current user’s profile and restart wsl (`wsl --shutdown`):

```ini
[wsl2]
memory=8GB
processors=4
swap=2GB
```

For performance issues, store container files inside WSL directory (Windows files are in /mnt/c).

For old kernels, one can enable compatibility with iptables:

```bash
sudo update-alternatives --config iptables
```

Docker can be ran from Windows command prompt by adding wsl before:

```docs
wsl docker images
```

## Applications

### Utilities

* KeePass
  * Plugins: [KeeTheme](https://github.com/xatupal/KeeTheme) (dark theme)
* WinDirStat

    ```dos
    winget install WinDirStat.WinDirStat
    ```
