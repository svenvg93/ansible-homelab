> [!IMPORTANT]
> This repository is a work in progress; I'm not an Ansible expert. Feel free to open PRs with improvements!

# 🧰 Ansible Homelab Automation

This repo automates the configuration of homelab servers using Ansible. It handles:

- 🐳 Docker installation
- 📡 Node Exporter for Prometheus metrics
- 🛡️ Beszel agent deployment and management
- 🧭 Tailscale VPN authentication
- 📊 Telegraf monitoring agent
- 🛠️ System maintenance tasks
- 🕰️ Timezone and basic system config

---

## 📁 Directory Structure

- `playbooks/` — Main playbooks for various tasks (e.g., `docker.yml`, `bootstrap.yml`)
- `roles/` — Ansible roles for modular configuration
- `inventory/hosts.yml` — Inventory file listing managed hosts
- `group_vars/` — Group variables, including secrets in `all/vault.yml`
- `.github/workflows/` — CI workflows for linting and testing

---

## 🖥️ Inventory Example

```yaml
all:
  hosts:
    pi4.tail43c135.ts.net: {}
    pi5.tail43c135.ts.net: {}
```

Hosts are typically referenced by their Tailscale or LAN DNS names.

---

## ▶️ Playbooks

Available playbooks in `playbooks/`:
- `beszel-agent.yml`
- `bootstrap.yml`
- `docker.yml`
- `maintenance.yml`
- `node-exporter.yml`
- `tailscale.yml`

Run a playbook with:
```sh
ansible-playbook -i inventory/hosts.yml playbooks/docker.yml
```

---

## 🔐 Secrets Management

Sensitive variables are stored in `group_vars/all/vault.yml` using [Ansible Vault](https://docs.ansible.com/ansible/latest/user_guide/vault.html). Example usage:

```sh
ansible-vault edit group_vars/all/vault.yml
```

**Note:** The actual vault file is encrypted and not human-readable.

---

## 🧪 Linting & Testing

- **Lint YAML:**
  ```sh
yamllint .
  ```
- **Lint Ansible:**
  ```sh
ansible-lint .
  ```
- **Syntax Check:**
  ```sh
ansible-playbook --syntax-check -i inventory/hosts.yml playbooks/docker.yml
  ```
- **Test Playbook (dry-run):**
  ```sh
ansible-playbook --check -i inventory/hosts.yml playbooks/docker.yml
  ```

---

## 🚀 Quickstart

1. Clone the repo and install requirements:
   ```sh
   ansible-galaxy install -r requirements.yml
   ```
2. Set up your inventory in `inventory/hosts.yml`.
3. Add secrets to `group_vars/all/vault.yml` (use `ansible-vault`).
4. Run a playbook:
   ```sh
   ansible-playbook -i inventory/hosts.yml playbooks/docker.yml
   ```

---

## 🤝 Contributing

PRs and suggestions are welcome!

---

## 🔧 Requirements

- Ansible 2.10+
- SSH access to all target hosts
- Python 3.x on control node
- Your hosts should be reachable via `.ts.net` (Tailscale) or LAN

