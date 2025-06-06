# Group Variables

All `group_vars` files live under the `group_vars/` directory. They allow you to set default values for variables used by roles.

```
group_vars/
├── all.yml
├── docker_hosts.yml
├── monitoring_hosts.yml
└── vpn_hosts.yml
```

### `group_vars/all.yml`

```yaml
# Global defaults
ansible_python_interpreter: /usr/bin/python3
timezone: "Europe/Amsterdam"

# Common credentials (make sure to use vault/encryption for secrets)
# ssh_user: "admin"
# ssh_private_key: "/home/you/.ssh/id_rsa"
```

* **`ansible_python_interpreter`**: ensures Python 3 is used on targets.
* **`timezone`**: sets timezone on all hosts unless overridden.

### `group_vars/docker_hosts.yml`

```yaml
docker_version: "20.10"
docker_users:
  - "dockeruser"
# If you need custom Docker CE repo URLs, override accordingly:
# docker_repo_url: "https://download.docker.com/linux/ubuntu"
```

* **`docker_version`**: major version to install (string).
* **`docker_users`**: list of Linux users to add to the `docker` group.

### `group_vars/monitoring_hosts.yml`

```yaml
# Node Exporter settings
node_exporter_version: "1.5.0"
node_exporter_port: 9100

# Telegraf settings
telegraf_version: "1.21.0"
telegraf_outputs:
  - name: "influxdb"
    url: "http://influxdb.local:8086"
    token: "YOUR_INFLUX_TOKEN"
    organization: "homeorg"
    bucket: "homelab"

# Choose which exporters/agents to install
install_node_exporter: true
install_telegraf: true
```

* **`node_exporter_version`**: version of Prometheus Node Exporter to install.
* **`telegraf_outputs`**: list of output configurations for Telegraf.
* **`install_node_exporter`** / **`install_telegraf`**: booleans to toggle installation.

### `group_vars/vpn_hosts.yml`

```yaml
tailscale_version: "1.38.5"
tailscale_auth_key: "tskey-XXXXXXXXXXXXXXXX"  # Should be stored securely (Ansible Vault)
tailscale_extra_args: "--advertise-routes=192.168.1.0/24"
```

* **`tailscale_auth_key`**: generated from your Tailscale admin panel (machine auth key).
* **`tailscale_extra_args`**: any extra flags for the `tailscale up` command.

> **Note:** If you override sensitive data (like `tailscale_auth_key` or `telegraf_outputs.token`), consider encrypting these files with [Ansible Vault](https://docs.ansible.com/ansible/latest/user_guide/vault.html).
