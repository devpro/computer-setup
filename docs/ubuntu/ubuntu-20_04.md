# Ubuntu 20.04 workstation setup

## Common packages

```bash
# refreshes the list of available updates
sudo apt update

# upgrades packages
sudo apt -y upgrade

# installs common dependencies
sudo apt install -y ca-certificates curl gnupg lsb-release apt-transport-https software-properties-common \
  git wget nano libarchive-tools sshpass zip unzip jq
```

## Software development

### .NET

- Register Microsoft's package repository (ref. [docs.microsoft.com](https://docs.microsoft.com/en-us/dotnet/core/install/linux-ubuntu))

```bash
declare repo_version=$(if command -v lsb_release &> /dev/null; then lsb_release -r -s; else grep -oP '(?<=^VERSION_ID=).+' /etc/os-release | tr -d '"'; fi)
wget https://packages.microsoft.com/config/ubuntu/$repo_version/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt update
```

- Install .NET SDK and display the version

```bash
sudo apt-get install -y dotnet-sdk-7.0
dotnet --version
```

### Go

- Download & install Go (ref. [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-go-on-ubuntu-20-04), [linuxhint](https://linuxhint.com/install-go-ubuntu-2/))

```bash
# installs latest version (https://go.dev/dl/)
curl -OL https://go.dev/dl/go1.19.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xvf go1.19.3.linux-amd64.tar.gz
rm go1.19.3.linux-amd64.tar.gz
```

- Configure Go in `~/.profile`

```ini
export PATH=$PATH:/usr/local/go/bin
```

- Apply profile changes

```bash
source ~/.profile
```

- Display version

```bash
go version
```

### Node.js & NPM

```bash
# (optional) removes Node.JS
sudo apt-get purge nodejs && rm -r /etc/apt/sources.list.d/nodesource.list
sudo apt autoremove

# installs Node.js 20 & NPM (ref. https://nodejs.org/en/download/package-manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash
nvm install 20
node -v
npm -v
```

### PHP

```bash
# installs PHP with APT
sudo add-apt-repository ppa:ondrej/php -y
sudo apt install php8.2
php --version

# installs PHP extensions
sudo apt install php8.2-{intl,mbstring,xml}

# installs Composer (see https://getcomposer.org/download/)
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e21205b207c3ff031906575712edab6f13eb0b361f2085f1f1237b7126d785e826a450292b6cfd1d64d92e6563bbde02') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
composer --version
```

### Python

- Install Python

```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
python --version
sudo apt install python3.11
python3.11 --version
```

- Configure Python version in `~/.bash_aliases` file (create it if it doesn't exist)

```ini
alias python=python3.11
```

- Apply profile changes

```bash
. ~/.bashrc
```

- Install pip (Python package manager)

```bash
# downloads the installation script and runs it with python
curl -sS https://bootstrap.pypa.io/get-pip.py | python

# makes sure latest pip has been installed
python -m pip install --upgrade pip
```

### Symfony

```bash
curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | sudo -E bash
sudo apt install symfony-cli
symfony check:requirements
```

→ [symfony.com/download](https://symfony.com/download)

## Infrastructure automation

### Ansible

```bash
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

→ [docs.ansible.com](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu)

### Terraform

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | \
    gpg --dearmor | \
    sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
    https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
    sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update
sudo apt-get install terraform
terraform -help
```

→ [Install Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)

## Containerization

### Docker

- Add Docker's official GPG key & install docker CLI (ref. [docs.docker.com/engine/install/ubuntu](https://docs.docker.com/engine/install/ubuntu/))

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce-cli docker-buildx-plugin
docker --version
```

- Install docker-compose (ref. [docs.docker.com/compose/install](https://docs.docker.com/compose/install/))

```bash
sudo apt-get install docker-compose-plugin
docker compose version
```

- Install Docker engine (ref. [Install Docker on WSL2 (Ubuntu)](https://dev.to/bartr/install-docker-on-windows-subsystem-for-linux-v2-ubuntu-5dl7))

```bash
sudo apt install -y docker-ce containerd.io

# adds the user to docker group so sudo won't be required
sudo usermod -aG docker ${USER}

# create docker daemon file to expose 2375 (insecure, see https://stackoverflow.com/questions/63416280/how-to-expose-docker-tcp-socket-on-wsl2-wsl-installed-docker-not-docker-deskt)
sudo sh -c 'echo {\"hosts\": [\"unix:///var/run/docker.sock\", \"tcp://0.0.0.0:2375\"]} > /etc/docker/daemon.json'

# starts docker service
sudo service docker start

# checks docker is running ok
sudo docker run --rm --name helloworld hello-world

# if there are issues you can look at log files
dmesg | grep docker
more /var/log/docker.log
```

- Edit `~/.profile` so Docker service is started if not running

```ini
if service docker status 2>&1 | grep -q "is not running"; then
  sudo service docker start
fi
```

- If Ubuntu is running in WSL2, run `sudo visudo` to add the following line at the end

```ini
# Docker
bthomas ALL = (root) NOPASSWD: /usr/sbin/service docker *
```

- Add alias in `~/.bash_aliases` file (create it if it doesn't exist)

```bash
alias trivy="docker run -it --rm -v trivy-cache:/root/.cache/ -v /var/run/docker.sock:/var/run/docker.sock:ro -v $HOME/.kube/config:/root/.kube/config aquasec/trivy:latest"
```

See also: [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04)

### Kubernetes

#### kubectl

- Official procedure

```bash
# adds GPG key (ref. https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
sudo curl -fsSLo /etc/apt/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

# installs
sudo apt-get update
sudo apt-get install -y kubectl

# setups autocomplete
source <(kubectl completion bash)
echo "source <(kubectl completion bash)" >> ~/.bashrc
alias k=kubectl
complete -F __start_kubectl k
```

→ [kubernetes.io/docs](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management)

- Azure procedure (to have kubeconfig, mandatory for clusters using Azure RBAC)

```bash
sudo az aks install-cli
```

→ [azure.github.io/kubelogin](https://azure.github.io/kubelogin/install.html)

#### krew

> Krew is the plugin manager for kubectl command-line tool

→ [krew.sigs.k8s.io](https://krew.sigs.k8s.io/)

- Download and install the binaries (ref. [Krew > Documentation > Installing](https://krew.sigs.k8s.io/docs/user-guide/setup/install/))

```bash
(
  set -x; cd "$(mktemp -d)" &&
  OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
  ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
  KREW="krew-${OS}_${ARCH}" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
  tar zxvf "${KREW}.tar.gz" &&
  ./"${KREW}" install krew
)
```

- Configure PATH in `~/.profile`

```ini
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
```

- Applies modifications to the terminal

```ini
source ~/.profile
```

#### kubectx & kubens

> **kubectx** is a tool to switch between contexts (clusters) on kubectl faster. **kubens** is a tool to switch between Kubernetes namespaces (and configure them for kubectl) easily.

→ [ahmetb/kubectx](https://github.com/ahmetb/kubectx)

```bash
kubectl krew install ctx
kubectl krew install ns
```

#### Helm

> The package manager for Kubernetes

→ [helm.sh](https://helm.sh/)

```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

#### K3s

/!\ won't work with WSL

```bash
curl -sfL https://get.k3s.io | sh -
```

#### Kind

/!\ isn't working with WSL2 and Rancher Desktop

> kind is a tool for running local Kubernetes clusters using Docker container “nodes”. kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

→ [kind.sigs.k8s.io](https://kind.sigs.k8s.io/), [code](https://github.com/kubernetes-sigs/kind)

- Download & install (ref. [Installing From Release Binaries](https://kind.sigs.k8s.io/docs/user/quick-start#installing-from-release-binaries))

```bash
# downloads and installs the binary (check the latest version available)
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.17.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

- Make a quick test

```bash
# checks kind is running ok
kind version
```

- Create a local cluster (see [Extra Port Mappings](https://kind.sigs.k8s.io/docs/user/configuration/#extra-port-mappings), [Using WSL2](https://kind.sigs.k8s.io/docs/user/using-wsl2/))

```bash
# creates a cluster
cat <<EOF | kind create cluster --config=-
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  extraPortMappings:
  - containerPort: 30000
    hostPort: 30000
    protocol: TCP
EOM

# (optional) creates a cluster to debug an issue
kind create cluster --retain
kind export logs

# lists clusters
kind get clusters

# sets kubectl context
kubectl cluster-info --context kind-kind

# deletes a cluster
kind delete cluster
```

- Create a cluster with Ingress (ref. [Kind > User Guide > Ingress](https://kind.sigs.k8s.io/docs/user/ingress/))

#### K3d

```bash
# runs installation script (ref. https://k3d.io/v5.5.2/#install-script)
wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

→ [Cheat sheet](https://everyday-cheatsheets.docs.devpro.fr/build/containers-and-cloud-native/kubernetes/k3d)

## Data stores

### MongoDB

```bash
sudo apt install mongo-tools
```

## Cloud providers

### Azure CLI

```bash
# uses the one-script install
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# logs in Azure interactively with the browser
az login
```

→ [Install the Azure CLI on Linux](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt)

## Collaboration

## tmate

```bash
sudo apt install tmate
```

→ [tmate.io](https://tmate.io/)

## Virtualization

### Packer

- Install with apt (ref. [packer.io](https://www.packer.io/downloads))

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install packer
```

### Vagrant

- Install Vagrant (ref. [vagrantup.com](https://www.vagrantup.com/downloads))

```bash
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update && sudo apt-get install vagrant
```

- Configure Vagrant to use VirtualBox from Windows host for WSL (ref. [vagrantup.com/docs/other/wsl](https://www.vagrantup.com/docs/other/wsl))

```bash
echo 'export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"' >> ~/.bashrc
echo 'export PATH="${PATH}:/mnt/c/Program Files/Oracle/VirtualBox"' >> ~/.bashrc
source ~/.bashrc
```

- Install Vagrant plugin for WSL2 (ref. [github.com/Karandash8/virtualbox_WSL2](https://github.com/Karandash8/virtualbox_WSL2))

```bash
vagrant plugin install virtualbox_WSL2
```

## Common actions

### Rename computer name

```bash
hostnamectl set-hostname 'new-hostname'
```
