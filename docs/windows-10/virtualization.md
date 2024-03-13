# Virtualization

## Hyper-V

### Ubuntu 22.04 Desktop on Hyper-V

Open Hyper-V, click on Quick create, select Ubuntu 22.04.

Connect to the machine and enable SSH.

```bash
sudo apt install openssh-server
ip -a
```

From Windows 10, connect to the machine:

```bash
ssh <myuser>@<localip>
```

### Ubuntu 22.04 Desktop on Hyper-V

Download iso file from [ubuntu.com/download/server](https://ubuntu.com/download/server) (`ubuntu-22.04.4-live-server-amd64.iso` for example).
