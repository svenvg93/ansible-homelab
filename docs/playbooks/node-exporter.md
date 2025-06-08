---
description: >-
  Deploy or uninstall Prometheus Node Exporter on hosts in the
  `monitoring_hosts` group.
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

1. Download and install the Node Exporter binary for the host’s architecture.
2. Create the node\_exporter system user and group.
3. Install and enable the systemd service unit (node\_exporter.service).
4. Start the Node Exporter service.
5. Reload the systemd daemon to pick up changes.

#### Uninstall

```
ansible-playbook -i inventory/hosts.yml playbooks/node_exporter.yml --tags uninstall
```

This will:

1. Stops and disables the node\_exporter service.
2. Removes the service unit file and binary.
3. Deletes the node\_exporter system user and group.
4. Reloads the systemd daemon.

### Related Files

* Role: `roles/node_exporter/`
* Uninstall Tasks: `roles/node_exporter/tasks/uninstall.yml`
* Playbook: `playbooks/node_exporter.yml`
