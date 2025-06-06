# Setup & Configuration

This section walks through how to configure inventory, group variables, and supporting files before running playbooks.

***

## Inventory Structure

See Inventory for details on how to list and group your hosts. At minimum, you should have:

```
inventory/
└── hosts.yml
```

Inside `hosts.yml`, define all your homelab machines and assign them to groups:

```yaml
all:
  children:
    docker_hosts:
      hosts:
        host1.ts.net:
        host2.ts.net:
    monitoring_hosts:
      hosts:
        host1.ts.net:
        host3.ts.net:
    vpn_hosts:
      hosts:
        host1.ts.net:
        host2.ts.net:
        host3.ts.net:
```

* `docker_hosts`: machines that should have Docker installed.
* `monitoring_hosts`: machines where Telegraf and/or Node Exporter will run.
* `vpn_hosts`: machines to enroll in Tailscale.

Adjust group names as desired, but keep them consistent with how roles expect to be applied.

***

## Group Variables

See Group Variables for all available variables and defaults. Typically, you will modify:

* `group_vars/docker_hosts.yml`
* `group_vars/monitoring_hosts.yml`
* `group_vars/vpn_hosts.yml`
* `group_vars/all.yml` (for global defaults, e.g. `timezone`, `ansible_python_interpreter`)

Use `host_vars/hostname.yml` sparingly for host‐specific overrides.

***

## Files Directory

The `files/` directory contains static files (e.g., Docker Compose templates, Telegraf config snippets, TLS certificates) that get copied to remote hosts. See Files Directory for details.
