---
description: Provision new machines with essential system setup and base roles.
---

# Bootstrap

### Roles Executed

* `bootstrap`: sets timezone, locale, SSH hardening and base packages
* `tailscale`: enrolls the host in the Tailscale VPN.
* `beszel`: installs the Beszel agent.
* `docker`: installs and configures Docker Engine and Docker Compose.
* `maintenance`: performs routine system maintenance tasks (updates, cleanup, pruning).

### Usage

Run the bootstrap playbook against one or more hosts:

```bash
ansible-playbook -i inventory/hosts.yml playbooks/bootstrap.yml
```

This will execute all the above roles in sequence on the target hosts.
