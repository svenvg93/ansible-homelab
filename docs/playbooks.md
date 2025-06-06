# Playbooks

All playbooks are located under the `playbooks/` directory:

```
playbooks/
├── docker.yml
├── monitoring.yml
├── vpn.yml
└── site.yml
```

### `playbooks/docker.yml`

```yaml
---
- name: Install and configure Docker on all docker_hosts
  hosts: docker_hosts
  become: true
  roles:
    - role: roles/docker
```

* Installs Docker Engine & Docker Compose.
* Adds specified `docker_users` to the `docker` group.
* Ensures Docker service is enabled and running.

### `playbooks/monitoring.yml`

```yaml
---
- name: Deploy monitoring agents (Node Exporter & Telegraf)
  hosts: monitoring_hosts
  become: true
  roles:
    - role: roles/node_exporter
      when: install_node_exporter | default(true)
    - role: roles/telegraf
      when: install_telegraf | default(true)
```

* **Node Exporter**: downloads and runs Prometheus Node Exporter as a systemd service.
* **Telegraf**: installs Telegraf, places `telegraf.conf`, and starts the agent.

### `playbooks/vpn.yml`

```yaml
---
- name: Enroll hosts into Tailscale
  hosts: vpn_hosts
  become: true
  roles:
    - role: roles/tailscale
```

* Installs Tailscale package (using the official apt/repo).
* Runs `tailscale up` with the provided `tailscale_auth_key` and any extra arguments.
* Ensures `tailscaled` is started and remains running.

### `playbooks/site.yml`

```yaml
---
- import_playbook: docker.yml
- import_playbook: monitoring.yml
- import_playbook: vpn.yml
```

* This is the “umbrella” playbook that runs all plays in sequence.
*   Run it with:

    ```bash
    ansible-playbook -i inventory/hosts.yml playbooks/site.yml
    ```

> **Tip:** If you want to run a single playbook (e.g., just VPN), use:
>
> ```bash
> ansible-playbook -i inventory/hosts.yml playbooks/vpn.yml
> ```
