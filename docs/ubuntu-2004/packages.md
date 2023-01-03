# Install Ubuntu 20.04 packages

## Package update

```bash
# refreshes the list of available updates
sudo apt update

# upgrades packages
sudo apt -y upgrade

# installs common dependencies
sudo apt install -y ca-certificates curl gnupg lsb-release apt-transport-https software-properties-common \
  git wget nano libarchive-tools sshpass zip unzip jq
```

## Programming languages

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

### Go

- Download & install Go (ref. [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-go-on-ubuntu-20-04), [linuxhint](https://linuxhint.com/install-go-ubuntu-2/))

```bash
# installs latest version (https://go.dev/dl/)
curl -OL https://go.dev/dl/go1.19.3.linux-amd64.tar.gz
sudo tar -C /usr/local -xvf go1.19.3.linux-amd64.tar.gz
rm go1.19.3.linux-amd64.tar.gz
```

- Configure Python in `~/.profile`

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

### Node.js

```bash
# installs Node.js & NPM (ref. https://github.com/nodesource/distributions/blob/master/README.md#debinstall)
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash - && sudo apt-get install -y nodejs
node --version
npm -v

# (optional) removes Node.JS
sudo apt-get purge nodejs && rm -r /etc/apt/sources.list.d/nodesource.list
sudo apt autoremove

# installs NVM (ref. https://github.com/nvm-sh/nvm#installing-and-updating)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
```

## Automation

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

#### Docker CLI & docker-compose

- Install as packages (ref. [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/))

```bash
# adds Docker’s official GPG key
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# uses the following command to set up the repository
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# updates the apt package index
sudo apt-get update

# installs the latest version of Docker CLI and Docker Compose
sudo apt-get install docker-ce-cli docker-compose-plugin
```

- Make a quick check

```bash
# displays version
docker --version
```

#### Docker from Rancher Desktop

- Fix permission error (see [Issue #1156](https://github.com/rancher-sandbox/rancher-desktop/issues/1156))

```bash
sudo groupadd docker
sudo adduser $USER docker
sudo chown root:docker /var/run/docker.sock
sudo chmod g+w /var/run/docker.sock
newgrp docker
```

### Kubernetes

#### kubectl

```bash
# adds GPG key (ref. https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

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
# runs installation script (ref. https://k3d.io/v5.4.6/#install-current-latest-release)
wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash
```

→ [Cheat sheet](https://everyday-cheatsheets.docs.devpro.fr/build/containers-and-cloud-native/kubernetes/k3d)

## Cloud Providers

### Azure CLI

```bash
# uses the one-script install
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# logs in Azure interactively with the browser
az login
```

→ [Install the Azure CLI on Linux](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt)
