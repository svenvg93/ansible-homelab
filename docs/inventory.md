# Inventory

Ansible’s inventory defines which machines to manage and how to group them. We use a single YAML file in this repo:

```
inventory/
└── hosts.yml
```

### Example `inventory/hosts.yml`

```yaml
all:
  children:
    # Group for Docker installation
    docker_hosts:
      hosts:
        host1.ts.net:
        host2.ts.net:

    # Group for Prometheus exporters & Telegraf
    monitoring_hosts:
      hosts:
        host1.ts.net:
        host3.ts.net:

    # Group for Tailscale VPN enrollment
    vpn_hosts:
      hosts:
        host1.ts.net:
        host2.ts.net:
        host3.ts.net:
```

* **`docker_hosts`**: all machines where Docker Engine and docker-compose will be installed.
* **`monitoring_hosts`**: hosts to install Node Exporter and/or Telegraf. May overlap with other groups.
* **`vpn_hosts`**: machines to enroll in Tailscale.

#### Tips

*   You can nest additional groups under `all > children`. For example:

    ```yaml
    all:
      children:
        web_servers:
          hosts:
            host4.ts.net:
        db_servers:
          hosts:
            host5.ts.net:
    ```

    If you do this, adjust `group_vars/` and plays accordingly.
* If you prefer an INI‐style inventory, rename `hosts.yml` to `hosts.ini` and adapt group names/format. All examples below assume YAML.
* Use `ansible-inventory --list -i inventory/hosts.yml` to verify that your inventory parses correctly.
