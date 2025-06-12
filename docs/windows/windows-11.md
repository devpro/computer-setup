# Windows 11

## Configuration

### Power options

Open `Control Panel` > `Hardware and Sound` >  `Power Options` > `Sytem Settings`.

In  `Shut-down settings`, check `Hibernate`.

### Display

Review and update:

Parameter                               | Path
----------------------------------------|----------------------------------------------------------------------------------------------------
HDR                                     | Settings (Windows) > System > Display > HDR (in Brightness & Colour)
Windows refresh rate (for every screen) | Settings (Windows) > System > Display > Advanced display (Related settings) > Choose a refresh rate
NVIDIA G-SYNC                           | NVIDIA Control Panel > Display > Set up G-SYNC > Enable G-SYNC
NVIDIA 3D program settings              | NVIDIA Control Panel > 3D Settings > Manage 3D settings > Program settings
NVIDIA application settings             | Settings (Windows) > System > Display > Graphics > Customised settings for applications

## Applications

### Utilities

* KeePass
  * Plugins: [KeeTheme](https://github.com/xatupal/KeeTheme) (dark theme)
* WinDirStat

    ```dos
    winget install WinDirStat.WinDirStat
    ```

### Windows Subsystem for Linux (WSL)

Open a dos window as Administrator to install the default Linux system (Ubuntu 24.04):

```dos
wsl --install
```

Ubuntu is now available in Windows Terminal.

Install Docker Engine (ref. [docs.docker.com/engine/install/ubuntu](https://docs.docker.com/engine/install/ubuntu/):

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker run hello-world
sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
```
