# Windows 10 workstation setup

## Drivers

* Intel
  * Intel Driver and Support Assistant
* Lenovo
  * Lenovo Service Bridge
  * Lenovo System Update
  * Lenovo Vantage
* NETGEAR
  * [NETGEAR Switch Discovery Tool (NSDT)](https://www.netgear.com/support/product/netgear-switch-discovery-tool)
* NVIDIA
  * NVIDIA Control Panel
  * NVIDIA RTX Desktop Manager

## Windows features

* `Containers`
* `Hyper-V`
  * Enable from a PowerShell terminal:

  ```ps1
  Get-WindowsFeature -Name Hyper-V
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
  ```

* `Windows Subsystem for Linux` (WSL)
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

## Windows optional features

* [OpenSSH](https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui#install-openssh-for-windows)

## Windows configuration

### Multiple GPU

* `Windows Settings` > `System` > `Display` > `Graphics settings` > `Graphics performance preference`
  * Select an application and explicitely set it to run on High performance

## Windows store

- `Microsoft Photos`
- `Microsoft Clipchamp`
- `Raw Image Extension`
  - Can be downloaded from [apps.microsoft.com](https://apps.microsoft.com/detail/9NCTDW2W1BH8)
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

## Applications

### Inventory

* [7-Zip](https://www.7-zip.org)
  * Unzip all files from a folder: `"C:\Program Files\7-Zip\7z.exe" e *.zip`
* Acrobat Reader
* [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/)
* [Balena Etcher](https://www.balena.io/etcher/) (cross-platform)
  * Alternative to create a bootable USD drive: [Rufus](https://rufus.ie/) (more functionalities)
    * [Create a bootable USB stick with Rufus on Windows](https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview)
* CPU-Z
* [Draw.io Desktop](https://github.com/jgraph/drawio-desktop)
* [Docker Desktop](https://www.docker.com/products/docker-desktop/)
  * Fix permission error (see [Issue #1156](https://github.com/rancher-sandbox/rancher-desktop/issues/1156))

  ```bash
  sudo groupadd docker
  sudo adduser $USER docker
  sudo chown root:docker /var/run/docker.sock
  sudo chmod g+w /var/run/docker.sock
  newgrp docker
  ```

  * Alternative: [Rancher Desktop](https://rancherdesktop.io/) ([docs](https://docs.rancherdesktop.io/), [GitHub](https://github.com/rancher-sandbox/rancher-desktop/))
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

* [Git for Windows](https://git-scm.com/download/win)
  * SSH key creation in `Git Bash` (see [Adding a new SSH key to your GitHub account](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/))

  ```bash
    # ED25519
  ssh-keygen -t ed25519 -C "firstname.lastname@email.com"

  # RSA
  ssh-keygen -t rsa -b 4096 -C "firstname.lastname@email.com"
  ```

  * Configure git (can be viewed & edited in `%userprofile%\.gitconfig`)

  ```bash
  # git config --global --edit
  git config --global core.longpaths true
  git config --global core.autocrlf false
  ```

* [GitKraken](https://www.gitkraken.com/)
* Google Chrome
  * Extensions: [Dark Reader](https://chrome.google.com/webstore/detail/dark-reader/eimadpbcbfnmbkopoojfekhnkhdbieeh?hl=en-US)
* [Greenshot](http://getgreenshot.org/downloads/)
* Java Runtime Environment (JRE)
* [KeePass](https://keepass.info/)
  * [Plugins](https://keepass.info/plugins.html): `KeePassHttp`
  * [Google extensions](https://chrome.google.com/webstore/category/extensions): `KeePassHttp-Connector`
* Make (2 options)
  * [MinGW](http://www.mingw.org/)
  * [GnuWin](http://gnuwin32.sourceforge.net/)
* [MariaDB Community Server](https://mariadb.com/downloads/community/) (to get the [GUI client](https://mariadb.com/docs/skysql/connect/clients/mariadb-client/))
* Microsoft Office
  * Outlook
    * [Change the temperature from Fahrenheit to Celsius](https://support.microsoft.com/en-au/office/change-the-temperature-from-fahrenheit-to-celsius-8303b0e2-644b-4ac3-954f-a478974b96c8)
    * [Add timezone](https://support.microsoft.com/en-us/office/add-remove-or-change-time-zones-5ab3e10e-5a6c-46af-ab48-156fedf70c04)
* minikube
* MongoDB Atlas CLI
* [MongoDB Compass](https://www.mongodb.com/products/compass)
* [Mozilla Firefox](https://www.mozilla.org/en-US/firefox/new/)
* [Node.js & NPM](https://nodejs.org/en/download/)
  * Edit files in nodejs folder to replace "-g" by "--location=global" (see [stackoverflow question #72401421](https://stackoverflow.com/questions/72401421/message-npm-warn-config-global-global-local-are-deprecated-use-loc))
  * Update packages

  ```bash
  # update packages
  npm update -g
  
  ## update NPM
  npm install npm@latest -g
  ```

* [Notepad++](https://notepad-plus-plus.org/)
* OpenVPN
* pgAdmin
* [Podman](https://podman.io/)
  * Download latest stable from [GitHub](https://github.com/containers/podman) releases page
  * Initalize a machine with `podman machine init` and start it with `podman machine start`
* [Postman](https://www.postman.com/)
* [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer)
* [Puppet Agent](https://www.puppet.com/docs/puppet/7/install_agents.html#install_windows_agents)
* [Puppet Development Kit](https://www.puppet.com/downloads/puppet-development-kit)
* [Ruby](https://www.ruby-lang.org/)

  ```bash
  # looks for the available versions
  winget search RubyInstallerTeam.Ruby

  # installs a specific version and restarts the terminal
  winget install RubyInstallerTeam.Ruby.3.2

  # makes sure ruby is available from the terminal
  ruby -v
  gem -v
  ```
  
* Slack
* [Vagrant](https://www.vagrantup.com/downloads)
  * Set `VAGRANT_DEFAULT_PROVIDER` environment variable to `virtualbox` or `hyperv` and restart Windows
  * Look at the [cheat sheet](https://everyday-cheatsheets.docs.devpro.fr/run/virtualization/vagrant)
* [VLC](https://www.videolan.org/vlc/)
* [VirtualBox]((https://www.virtualbox.org/wiki/Downloads))
* [Visual Studio Code](https://code.visualstudio.com/)
  * Extensions: `CMake Language Support`, `CSS Formatter`, `Debbuger for Firefox`, `Dev Containers`, `Docker`, `EditorConfig for VS Code`, `Go`, `HashiCorp Terraform`, `Kubernetes`, `Markdown Table Pretifier`, `markdownlint`, `MongoDB for VS Code`, `WSL`, `YAML`
  * `setttings.json`:
 
  ```json
  {
    "editor.minimap.enabled": false,
    "security.workspace.trust.untrustedFiles": "open",
    "redhat.telemetry.enabled": false,
    "mdb.confirmRunAll": false,
    "[markdown]": {
      "editor.defaultFormatter": "DavidAnson.vscode-markdownlint"
    },
    "terminal.integrated.defaultProfile.windows": "Command Prompt",
    "[python]": {
      "editor.formatOnType": true
    },
    "playwright.reuseBrowser": true,
    "vs-kubernetes": {
      "vs-kubernetes.crd-code-completion": "disabled"
    },
    "workbench.colorTheme": "Visual Studio Dark",
    "typescript.updateImportsOnFileMove.enabled": "always",
    "git.openRepositoryInParentFolders": "never",
    "puppet.installDirectory": "C:\\Programs\\PuppetDevelopmentKit",
    "puppet.installType": "pdk",
  }
  ```
  
* [Visual Studio 2022](https://visualstudio.microsoft.com/vs/community/)
  * Self-generated certificate for .NET (ref. [stackoverflow.com/questions/56409580](https://stackoverflow.com/questions/56409580/trouble-trusting-local-https-certificate-in-asp-net-core))
    * Execute "certlm.msc" to open the certificate manager
    * Go to Personal/Certificates and locate localhost certificate
    * Move the certificate to "Trusted Root Certification Authorities/Certificates"
* VLC
* [wget](https://www.gnu.org/software/wget/)
  * solution found on [GitHub](https://github.com/cmderdev/cmder/issues/69)
  * as indicated in the [faq](https://www.gnu.org/software/wget/faq.html#download) go to [eternallybored.org/misc/wget](https://eternallybored.org/misc/wget/) and download the latest x64 version
  * extract the exe file and copy it in your local cmder installation bin directory
* [WinMerge](https://winmerge.org/)
* [zoomit](https://docs.microsoft.com/en-us/sysinternals/downloads/zoomit)

### Binaries in PATH

* [Docker CLI](https://github.com/StefanScherer/docker-cli-builder/releases)
  * Create an environment variable to access Docker engine running on WSL

  Key         | Value
  ----------- | --------------------
  DOCKER_HOST | tcp://localhost:2375

  * Make a check (the output doesn't display during the run, strange...)
  
  ```bash
  docker run --name helloworld hello-world
  docker logs helloworld
  docker rm helloworld
  ```
  
* [Helm](https://helm.sh/docs/intro/install/)
* [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/)
* kubeseal
* mongosh
* [PsExec](https://learn.microsoft.com/en-us/sysinternals/downloads/psexec)
  * Run as a service account: `psexec -i -s cmd.exe`
* Terraform

### Chocolatey packages

* Install applications with Chocolatey (package manager for Windows)

```ps1
# installs Chocolatey
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# installs Firefox
choco install -y firefox

# installs Windows Terminal
choco install -y microsoft-windows-terminal

# VSCode + Extensions (an example provided here)
choco install -y vscode --params "/NoDesktopIcon"
code --install-extension ms-vscode.powershell

# installs git client
choco install -y git.install --params "/GitOnlyOnPath /NoAutoCrlf /NoShellIntegration"

# installs .NET Framework 4.8 developer pack
choco install -y netfx-4.8-devpack

# installs latest .NET SDK (6.0 in October 2022)
choco install -y dotnet-sdk

# installs Visual Studio 2022 Build tools & NuGet
choco install -y visualstudio2022buildtools nuget.commandline

# installs Notepad++
choco install -y notepadplusplus
```

### Utilities

#### Hard Drive Backup

* [Unstoppable Copier](https://www.roadkil.net/)

### Oldies

* ACDSee
* CCleaner
* ColorPic
* DaemonTools
* Everest Ultimate
* FileZilla
* Gadwin PrintScreen
* HDGraph
* K-Lite Codec Pack
* Magic Draw
* Partition Magic
* PDF Creator
* Picasa
* QuickTime
* TestDisk
* Toad
* UltraEdit
* VirtualDub
* Winamp
* XML Spy

## Configuration

* Control Panel / User Accounts /Credential Manager
