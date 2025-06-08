---
description: Perform routine system maintenance tasks on all hosts.
---

# Maintenance

### Roles

* `maintenance`: updates packages, cleans up old logs, prunes Docker resources, and vacuums journal logs.

### Usage

```bash
ansible-playbook -i inventory/hosts.yml playbooks/maintenance.yml
```

This will:

1. Update and upgrade system packages.
2. Clean the APT cache.
3. Prune unused Docker images, containers, volumes, and networks.
4. Vacuum journal logs older than a specified retention period.
5. Remove old log files under `/var/log` older than a specified age.
