# Windows applicatons

## Windows features

* `Containers`
* `Hyper-V`
  * Enable from a PowerShell terminal:

  ```ps1
  Get-WindowsFeature -Name Hyper-V
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
  ```

* `Windows subsystem for Linux` (WSL)
  * Review and configure WSL from the command line

  ```cmd
  REM displays installed linux systems
  wsl -l -v

  REM sets default to version 2
  wsl --set-default-version 2
  
  REM updates the system (can fix start errors)
  wsl.exe --update
  ```

  * Configure the access to WSL from Windows

  ```ps
  REM adds a firewall rule to enable inbound from WSL
  New-NetFirewallRule -DisplayName "WSL" -Direction Inbound -InterfaceAlias "vEthernet (WSL)" -Action Allow
  ```
  
# Windows store

- `Microsoft Photos`
- `Ubuntu on Windows`
  - Once installed, look at [Ubuntu setup]([#ubuntu-2004](https://devpro.github.io/workstation-setup/docs/ubuntu-2004/packages.html))
  - Open a shell in Ubuntu and create or update `/etc/wsl.conf` file to enable chmod (required for SSH) and avoid issues with npm commands (see [Advanced settings configuration in WSL](https://docs.microsoft.com/en-us/windows/wsl/wsl-config))

  ```ini
  # /etc/wsl.conf
  [automount]
  options = "metadata"

  [interop]
  appendWindowsPath = false
  ```

  - Restart WSL from Windows

  ```bash
  wsl --shutdown
  ```

  - Copy SSH key (must be generated before in Windows with Git Bash for example) and review permissions (see [Sharing SSH keys between Windows and WSL 2](https://devblogs.microsoft.com/commandline/sharing-ssh-keys-between-windows-and-wsl-2/))

  ```bash
  cp -r /mnt/c/Users/<myusername>/.ssh/id_rsa* ~/.ssh/
  chmod 700 ~/.ssh/
  chmod 644 ~/.ssh/*.pub
  chmod 600 ~/.ssh/id_ed25519
  chmod 600 ~/.ssh/id_rsa
  ```

- [Windows Terminal](https://github.com/microsoft/terminal)
  - Download the msixbundle file from the latest release
  - Execute in PowerShell `Add-AppxPackage .\Microsoft.WindowsTerminal_Win10_xxx.msixbundle`

- [Winget](https://github.com/microsoft/winget-cli) ([docs](https://docs.microsoft.com/en-us/windows/package-manager/winget/))
  - Download the msixbundle file and licence from the latest release
  - Execute in PowerShell `Add-AppxProvisionedPackage -online -PackagePath .\Microsoft.DesktopAppInstaller_xxx.msixbundle -LicensePath .\xxx_License1.xml`
  - Double check it works with `winget list`
  - If needed, you can look at the package with `Get-AppxPackage microsoft.desktopappinstaller` and uninstall it with `Remove-AppxPackage -Package Microsoft.DesktopAppInstaller_xxx`

## Inventory

* 7-zip
  * Unzip all files from a folder: `"C:\Program Files\7-Zip\7z.exe" e *.zip`
* Acrobat Reader
* [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/)
* CPU-Z
* [Draw.io Desktop](https://github.com/jgraph/drawio-desktop)
* Docker Engine
  * Install from a Powershell terminal ([Prepare Windows for containers](https://learn.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment)):

  ```ps1
  Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1
  .\install-docker-ce.ps1
  ```
  
  * Review Docker configuration: `C:\ProgramData\docker\config\daemon.json`
  * Start Docker

  ```dos
  "C:\Programs\docker-20.10.19\docker\dockerd.exe" -H npipe:////./pipe/docker_windows
  ```

  * Create Docker context from the original terminal

  ```dos
  docker context create win --docker host=npipe:////./pipe/docker_windows
  ```

  * Use Docker context from another terminal as an Administrator

  ```dos
  docker -c win ps
  ```

* [Etcher](https://www.balena.io/etcher/)
  * [Create a bootable USB stick with Rufus on Windows](https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview)
* [Git for Windows](https://git-scm.com/download/win)
  * SSH key creation in `Git Bash` (see [Adding a new SSH key to your GitHub account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/))

  ```bash
    # ED25519
  ssh-keygen -t ed25519 -C "firstname.lastname@email.com"

  # RSA
  ssh-keygen -t rsa -b 4096 -C "firstname.lastname@email.com"
  ```

* [GitKraken](https://www.gitkraken.com/)
* Google Chrome
  * Extensions: [Dark Reader](https://chrome.google.com/webstore/detail/dark-reader/eimadpbcbfnmbkopoojfekhnkhdbieeh?hl=en-US)
* [Greenshot](http://getgreenshot.org/downloads/)
* [Helm](https://helm.sh/docs/intro/install/)
* Intel Driver and Support Assistant
* JRE
* KeePass (or any other secret manager)
* [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/)
* Make (2 options)
  * [MinGW](http://www.mingw.org/)
  * [GnuWin](http://gnuwin32.sourceforge.net/)
* [MariaDB Community Server](https://mariadb.com/downloads/community/) (to get the [GUI client](https://mariadb.com/docs/skysql/connect/clients/mariadb-client/))
* Microsoft Office
  * Outlook
    * [Change the temperature from Fahrenheit to Celsius](https://support.microsoft.com/en-au/office/change-the-temperature-from-fahrenheit-to-celsius-8303b0e2-644b-4ac3-954f-a478974b96c8)
    * [Add timezone](https://support.microsoft.com/en-us/office/add-remove-or-change-time-zones-5ab3e10e-5a6c-46af-ab48-156fedf70c04)
* minikube
* [MongoDB Compass](https://www.mongodb.com/products/compass)
* Mozilla Firefox
* [NPM](https://nodejs.org/en/download/)
  * Edit files in nodejs folder to replace "-g" by "--location=global" (see [stackoverflow question #72401421](https://stackoverflow.com/questions/72401421/message-npm-warn-config-global-global-local-are-deprecated-use-loc))
  * Update packages

  ```bash
  # update packages
  npm update -g
  
  ## update NPM
  npm install npm@latest -g
  ```

* [Notepad++](https://notepad-plus-plus.org/)
* [OBS Studio](https://obsproject.com/fr/)
* [OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_overview)
* [Podman](https://podman.io/)
  * Download latest stable from [GitHub](https://github.com/containers/podman) releases page
  * Initalize a machine with `podman machine init` and start it with `podman machine start`
* [Postman](https://www.postman.com/)
* Process Explorer
* [PsExec](https://learn.microsoft.com/en-us/sysinternals/downloads/psexec)
  * Run as a service account: `psexec -i -s cmd.exe`
* [Rancher Desktop](https://rancherdesktop.io/) ([docs](https://docs.rancherdesktop.io/), [GitHub](https://github.com/rancher-sandbox/rancher-desktop/))
* Steam
* Ubisoft Connect
* Vagrant
* [VLC](https://www.videolan.org/vlc/)
* VirtualBox
* [Visual Studio Code](https://code.visualstudio.com/)
  * Extensions: `EditorConfig for VS Code`, `Markdown Table Pretifier`, `markdownlist`, `YAML`
* Visual Studio 2022
* [wget](https://www.gnu.org/software/wget/)
  * solution found on [GitHub](https://github.com/cmderdev/cmder/issues/69)
  * as indicated in the [faq](https://www.gnu.org/software/wget/faq.html#download) go to [eternallybored.org/misc/wget](https://eternallybored.org/misc/wget/) and download the latest x64 version
  * extract the exe file and copy it in your local cmder installation bin directory
* WinMerge
* [zoomit](https://docs.microsoft.com/en-us/sysinternals/downloads/zoomit)

### Chocolatey packages

- (Optional) Install applications with Chocolatey (package manager for Windows)

```ps1
# installs Chocolatey
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# installs git client
choco install -y git

# installs .NET Framework 4.8 developer pack
choco install -y netfx-4.8-devpack

# installs latest .NET SDK (6.0 in October 2022)
choco install -y dotnet-sdk

# installs Visual Studio 2022 Build tools & NuGet
choco install -y visualstudio2022buildtools nuget.commandline

# installs Notepad++
choco install notepadplusplus
```
