---
description: Deploy or uninstall Prometheus Node Exporter
---

# Node Exporter

### Roles

* &#x20;`node_exporter`: &#x20;
  * Downloads and installs the Node Exporter binary. &#x20;
  * Sets up a systemd service and user. &#x20;
  * Manages architecture‐specific releases.

### Tasks

#### Installation (default)

```
ansible-playbook -i inventory/hosts.yml playbooks/node_exporter.yml
```

This will:
- Download and install the Node Exporter binary for the host’s architecture.
- Create the `node_exporter` system user and group.
- Install and enable the systemd service unit (`node_exporter.service`).
- Start the Node Exporter service.
- Reload the systemd daemon to pick up changes.

#### Uninstall

```
ansible-playbook -i inventory/hosts.yml playbooks/node_exporter.yml --tags uninstall
```

This will:
- Stop and disable the `node_exporter` service.
- Remove the service unit file and binary.
- Delete the `node_exporter` system user and group.
- Reload the systemd daemon.

### Related Files

* Role: `roles/node_exporter/`
* Uninstall Tasks: `roles/node_exporter/tasks/uninstall.yml`
* Playbook: `playbooks/node_exporter.yml`
