Grafana Agent Role
==================

This Ansible role installs and configures the Grafana Agent to collect and ship logs to a Loki endpoint.

Requirements
------------
- Target hosts must have Internet access to download the Grafana Agent binary.
- `unzip` and `curl` packages are required (the role will install them via APT).
- Systemd must be available to manage the Grafana Agent service.

Role Variables
--------------
Available variables are listed below, along with their default values (see `defaults/main.yml`):

- `grafana_agent_version` (string): Version of the Grafana Agent to install.  
  Default: `0.28.4`
- `grafana_agent_download_base` (string): Base URL for downloading Grafana Agent releases.  
  Default: `https://github.com/grafana/agent/releases/download/v{{ grafana_agent_version }}`
- `grafana_agent_arch` (string): CPU architecture for the binary (set automatically from `ansible_architecture`).
- `grafana_agent_download_url` (string): Full download URL for the Grafana Agent zip archive.
- `grafana_agent_install_dir` (string): Directory to install the Grafana Agent.  
  Default: `/opt/grafana-agent`
- `loki_address` (string): URL for the Loki push API.  
  Default: `http://localhost:3100/loki/api/v1/push`
- `agent_log_paths` (list): List of file paths or glob patterns to tail for shipping logs.  
  Default:
  ```yaml
  agent_log_paths:
    - "/var/log/*.log"
  ```

Dependencies
------------
None.

Example Playbook
----------------
```yaml
- hosts: all
  become: yes
  vars:
    loki_address: "http://loki.mycompany.com:3100/loki/api/v1/push"
    agent_log_paths:
      - "/var/log/auth.log"
      - "/var/log/syslog"
  roles:
    - grafana_agent
```

License
-------
MIT

Author Information
------------------
Created by Sven.  
GitHub: https://github.com/yourusername
Email: your.email@example.com
