> [!IMPORTANT]
> This repository is a work in progress; I’m not an Ansible expert. Feel free to open PRs with improvements!

# 🧰 Ansible Homelab Automation

This repo automates the configuration of homelab servers using Ansible. It handles:

- 🐳 Docker installation
- 📡 Node Exporter for Prometheus metrics
- 🛡️ Beszel agent deployment and management
- 🧭 Tailscale VPN authentication
- 📊 Telegraf monitoring agent
- 🛠 System maintenance tasks
- 🕰 Timezone and basic system config

---

## 🔧 Requirements

- Ansible 2.10+
- SSH access to all target hosts
- Python 3.x on control node
- Your hosts should be reachable via `.ts.net` (Tailscale) or LAN

