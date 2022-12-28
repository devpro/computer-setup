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

### kubectx & kubens

* [ahmetb/kubectx](https://github.com/ahmetb/kubectx)
