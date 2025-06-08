---
description: >-
  Install and run the Ookla Speedtest CLI to measure network performance on all
  hosts.
---

# Ookla Speedtest

### Roles

\- `speedtest`: &#x20;

&#x20; \- Installs the Speedtest CLI package. &#x20;

&#x20; \- Configures and schedules periodic runs (via cron or systemd timer). &#x20;

&#x20; \- Collects and optionally pushes results to your monitoring system.

### Task

#### Installation (default)

```
ansible-playbook -i inventory/hosts.yml playbooks/ookla-speedtest.yml
```

This will:

* Install the Speedtest CLI on each host.
* Schedule and execute periodic speed tests according to the role’s defaults.
* Store results locally (or forward them, if you’ve configured outputs).

### Related files

* Role: `roles/speedtest/`
* Playbook: `playbooks/ookla-speedtest.yml`
