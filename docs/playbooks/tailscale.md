# Tailscale

### Purpose

Enroll hosts into the Tailscale VPN network and configure connectivity.

### Roles

* `tailscale`: installs the Tailscale client, runs `tailscale up` with provided auth key and extra arguments, and ensures the `tailscaled` service is enabled and running.

### Variables

Ensure the following variables are set (in `inventory/group_vars/tailscale_hosts/vault.yml` or similar):

* `tailscale_auth_key` (string, **vaulted**): Your Tailscale machine auth key.

<details>

<summary><strong>🔒 Vault Setup</strong></summary>

Create an encrypted vault for the Tailscale auth key:

```bash
ansible-vault create inventory/group_vars/tailscale_hosts/vault.yml
```

Inside the file, enter:

```yaml
tailscale_auth_key: "tskey-XXXXXXXXXXXXXXXX"
```

</details>

### Tasks

#### Installation (default)

```bash
ansible-playbook -i inventory/hosts.yml playbooks/tailscale.yml
```

This will:

* Install or update the Tailscale package on each host.
* Authenticate and join the host to your Tailscale network using the `tailscale_auth_key`.
* Enable and start the `tailscaled` systemd service.

#### Enabling Tailscale SSH (optional)

```
ansible-playbook -i inventory/hosts.yml playbooks/tailscale.yml --tags tailscale_ssh
```

This will:

* Run `tailscale up --ssh` to enable SSH over Tailscale (only if the host is already authenticated).

### Related files

* **Role:** `roles/tailscale/`
* **Playbook:** `playbooks/tailscale.yml`
