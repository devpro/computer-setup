# Virtualization

## Hyper-V

### Ubuntu 22.04 Desktop on Hyper-V

Open Hyper-V, click on Quick create, select Ubuntu 22.04.

Connect to the machine and enable SSH.

```bash
sudo apt install openssh-server
ip a
```

To access it from WSL, you first need to enable the network forwarding, execute the command from a PowerShell window ran as an Admin (solution found at [stackoverflow.com/questions/61868920](https://stackoverflow.com/questions/61868920/connect-hyper-v-vm-from-wsl-ubuntu)):

```ps1
Get-NetIPInterface | where {$_.InterfaceAlias -eq 'vEthernet (WSL)' -or $_.InterfaceAlias -eq 'vEthernet (Default Switch)'} | Set-NetIPInterface -Forwarding Enabled
```

From Windows 10, connect to the machine:

```bash
ssh <myuser>@<localip>
```

### Ubuntu 22.04 Desktop on Hyper-V

Download iso file from [ubuntu.com/download/server](https://ubuntu.com/download/server) (`ubuntu-22.04.4-live-server-amd64.iso` for example).
