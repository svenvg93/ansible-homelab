---
description: Install and configure Docker Engine and Docker Compose on all hosts.
---

# Docker

### Roles

* `docker`: handles installing Docker packages, configuring the Docker group, and deploying any Docker Compose templates.

### Tasks

#### Installation (default)

```bash
ansible-playbook -i inventory/hosts.yml playbooks/docker.yml
```

This will:

1. Add the Docker repository and GPG key.
2. Install `docker-ce`, `docker-ce-cli`, `containerd.io`, and Docker Compose.
3. Add specified users to the `docker` group.
4. Enable and start the Docker service.

#### Uninstall

```
ansible-playbook -i inventory/hosts.yml playbooks/docker.yml --tags uninstall
```

This will:

1. Stop and disable the Docker service.
2. Remove the Docker packages (docker-ce, docker-ce-cli, containerd.io).
3. Delete the docker group.
4. Autoremove unused packages and clean the APT cache.
