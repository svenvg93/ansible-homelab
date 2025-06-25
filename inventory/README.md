# Inventory Structure

This directory contains the Ansible inventory for your homelab.

## Structure
- `hosts.yml`: Main inventory file. Defines all hosts and groups.
- `group_vars/`: Variables shared by groups of hosts.
- `host_vars/`: Variables specific to individual hosts (optional).

## Example: hosts.yml
```yaml
all:
  hosts:
    pi4.tail43c135.ts.net: {}
    pi5.tail43c135.ts.net: {}
  children:
    docker:
      hosts:
        pi4.tail43c135.ts.net:
        pi5.tail43c135.ts.net:
    monitoring:
      hosts:
        pi4.tail43c135.ts.net:
```

## Adding a Host
- Add the hostname under `all.hosts`.
- Assign it to one or more groups under `children` as needed.

## Group Usage
- Use groups to target playbooks/roles to specific sets of hosts (e.g., `docker`, `monitoring`).

## Best Practices
- Use FQDNs or Tailscale/LAN DNS names for hosts.
- Store secrets in `group_vars/all/vault.yml` using Ansible Vault. 