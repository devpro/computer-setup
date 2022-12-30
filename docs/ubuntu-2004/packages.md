# Install Ubuntu 20.04 packages

## Common

```bash
sudo apt update
sudo apt install software-properties-common
sudo apt install -y jq
```

## Automation

### Ansible

```bash
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

→ [docs.ansible.com](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu)

## Kubernetes

### kubectl

### krew

> Krew is the plugin manager for kubectl command-line tool

→ [krew.sigs.k8s.io](https://krew.sigs.k8s.io/)

- Download and install the binaries

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

Ref. [Krew > Documentation > Installing](https://krew.sigs.k8s.io/docs/user-guide/setup/install/).

### kubectx & kubens

> **kubectx** is a tool to switch between contexts (clusters) on kubectl faster. **kubens** is a tool to switch between Kubernetes namespaces (and configure them for kubectl) easily.

→ [ahmetb/kubectx](https://github.com/ahmetb/kubectx)

```bash
kubectl krew install ctx
kubectl krew install ns
```
