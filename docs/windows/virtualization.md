# Virtualization

## Hyper-V

### Ubuntu 22.04 Desktop on Hyper-V

Open Hyper-V, click on Quick create, select Ubuntu 22.04.

Connect to the machine, enable SSH and set a fixed IP.

```bash
sudo apt install openssh-server
ip a
sudo vi /etc/netplan/01-network-manager-all.yaml
sudo netplan apply
```

Example of configuration:

```yaml
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    eth0:
      addresses:
        - 172.19.147.10/20
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
      routes:
        - to: default
          via: 172.19.144.1
```

To access it from WSL, you first need to enable the network forwarding, execute the command from a PowerShell window ran as an Admin (solution found at [stackoverflow.com/questions/61868920](https://stackoverflow.com/questions/61868920/connect-hyper-v-vm-from-wsl-ubuntu)):

```ps1
Get-NetIPInterface | where {$_.InterfaceAlias -eq 'vEthernet (WSL)' -or $_.InterfaceAlias -eq 'vEthernet (Default Switch)'} | Set-NetIPInterface -Forwarding Enabled
```

From Windows 10, connect to the machine:

```bash
ssh <myuser>@<localip>
```
