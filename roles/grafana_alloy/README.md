# Grafana Alloy Role

This role installs and configures Grafana Alloy to collect system logs and ship them to a Loki endpoint. It supports both x86_64 and ARM (arm64, armv7) systems automatically.

## Features
- Installs Grafana Alloy (latest or specified version)
- Automatically selects the correct binary for x86_64, arm64, or armv7 architectures
- Configures Alloy to collect system logs from /var/log and journald
- Ships logs to a specified Loki endpoint with optional authentication
- Manages the Alloy systemd service (user, group, and extra options are configurable)

## Role Variables
| Variable                        | Default                                         | Description                                      |
|----------------------------------|-------------------------------------------------|--------------------------------------------------|
| `grafana_alloy_version`          | latest                                          | Version of Alloy to install                       |
| `grafana_alloy_loki_url`         | http://loki.example.com:3100/loki/api/v1/push   | Loki endpoint URL                                 |
| `grafana_alloy_loki_tenant_id`   | ""                                             | Loki tenant ID (optional)                         |
| `grafana_alloy_loki_username`    | ""                                             | Loki username (optional)                          |
| `grafana_alloy_loki_password`    | ""                                             | Loki password (optional)                          |
| `grafana_alloy_config_path`      | /etc/alloy/config.yaml                          | Path to Alloy config file                         |
| `grafana_alloy_service_name`     | alloy                                           | Name of the Alloy systemd service                 |
| `grafana_alloy_user`             | alloy                                           | User to run the Alloy service                     |
| `grafana_alloy_group`            | alloy                                           | Group to run the Alloy service                    |
| `grafana_alloy_extra_opts`       | ""                                             | Extra command-line options for Alloy              |

## Multi-Architecture Support
The role automatically detects the system architecture (`ansible_architecture`) and downloads the correct Alloy binary for:
- x86_64 / amd64
- arm64 / aarch64
- armv7l / armhf

You do not need to set the download URL manually; it is handled by the role.

## Example Playbook
```yaml
- hosts: all
  become: true
  roles:
    - role: grafana_alloy
      vars:
        grafana_alloy_loki_url: "http://loki.yourdomain.com:3100/loki/api/v1/push"
        grafana_alloy_loki_username: "lokiuser"
        grafana_alloy_loki_password: "supersecret"
        grafana_alloy_user: "alloy"
        grafana_alloy_group: "alloy"
        grafana_alloy_extra_opts: "--log.level=debug"
```

## License
MIT-0

## Author
Your Name <your.email@example.com> 