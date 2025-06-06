# Requirements

Before you begin, ensure the following are in place:

* **Control Node** (your laptop or a central server):
  * Ansible 2.10 or later
  * Python 3.6+ (and `pip3`)
  * SSH key pair that can log into all target hosts
  * Network connectivity to all target hosts (either via LAN or Tailscale)
* **Target Hosts** (your homelab servers/VMs):
  * SSH server installed and running
  * A non‐root user with `sudo` privileges (recommended)
  * Python 3.x installed (so Ansible’s Python modules can run)
  * Reachable by hostname (e.g., `host1.ts.net` if using Tailscale or `192.168.1.10` on LAN)

Additional notes:

* If you plan to use **Tailscale** for VPN, each host should have Tailscale installed beforehand or use the `tailscale` role provided.
* Docker will be installed on machines included in the `docker_hosts` group. Ensure they meet Docker Engine’s OS requirements.
* By default, this repo uses YAML‐formatted inventories (`.yml`). You can switch to INI format by renaming files, but all examples assume YAML.
