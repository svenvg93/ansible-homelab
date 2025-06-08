# Playbooks

All playbooks are located under the `playbooks/` directory:

- [Docker](docker-playbook.md)
- [Monitoring](monitoring-playbook.md)
- [VPN (Tailscale)](tailscale-playbook.md)
- [Site](site-playbook.md)
- [Beszel Agent](bezsel-agent-playbook.md)
- [Bootstrap](bootstrap-playbook.md)
- [cAdvisor Deploy](cadvisor-deploy-playbook.md)
- [Maintenance](maintenance-playbook.md)
- [Node Exporter](node-exporter-playbook.md)
- [Ookla Speedtest](ookla-speedtest-playbook.md)

```
playbooks/
├── docker.yml
├── monitoring.yml
├── vpn.yml
└── site.yml
```

### `playbooks/docker.yml`

```yaml
- name: Install and configure Docker on all docker_hosts
  hosts: docker_hosts
  become: true
  roles:
    - role: docker
```

* Installs Docker Engine & Docker Compose.
* Adds specified `docker_users` to the `docker` group.
* Ensures Docker service is enabled and running.

### `playbooks/monitoring.yml`

```yaml
- name: Deploy monitoring agents (Node Exporter & Telegraf)
  hosts: monitoring_hosts
  become: true
  roles:
    - role: node_exporter
      when: install_node_exporter | default(true)
    - role: telegraf
      when: install_telegraf | default(true)
```

* **Node Exporter**: downloads and runs Prometheus Node Exporter as a systemd service.
* **Telegraf**: installs Telegraf, places `telegraf.conf`, and starts the agent.

### `playbooks/tailscale.yml`

```yaml
- name: Enroll hosts into Tailscale
  hosts: vpn_hosts
  become: true
  roles:
    - role: tailscale
```

* Installs Tailscale package (using the official apt/repo).
* Runs `tailscale up` with the provided `tailscale_auth_key` and any extra arguments.
* Ensures `tailscaled` is started and remains running.

### `playbooks/site.yml`

```yaml
- import_playbook: docker.yml
- import_playbook: monitoring.yml
- import_playbook: vpn.yml
```

* This is the “umbrella” playbook that runs all plays in sequence.
*   Run it with:

    ```bash
    ansible-playbook -i inventory/hosts.yml playbooks/site.yml
    ```

> **Tip:** If you want to run a single playbook (e.g., just Tailscale), use:
>
> ```bash
> ansible-playbook -i inventory/hosts.yml playbooks/taiscale.yml
> ```
