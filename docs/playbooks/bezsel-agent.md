---
description: Install or uninstall the Beszel agent on hosts in the `beszel_hosts` group.
---

# Bezsel Agent

### Roles

\- `bezsel`: handles download, installation (with optional auto-update), and removal of the agent.

### Variables

\- `beszel_agent_ssh_port` (integer): SSH port used by the agent (default in \`defaults/main.yml\`).
\- `beszel_agent_ssh_key` (string, **vaulted**): Public key for agent authentication, loaded from  `inventory/group_vars/beszel_hosts/vault.yml`.
\- `beszel_agent_autoupdate` (boolean): If \`true\`, enables agent’s auto-update feature.

{% hint style="info" %}
Don't forget to create your vault file with the `beszel_agent_ssh_key`
{% endhint %}

<details>

<summary><strong>🔒 Vault Setup</strong></summary>

Run the following command to create your encrypted vault:

```
ansible-vault create inventory/group_vars/beszel_hosts/vault.yml
```

In the editor that opens, enter:

```
beszel_agent_ssh_key: "ssh-ed25519 AAAA…"
```

</details>

### Tasks

#### Installation (default)

```
ansible-playbook -i inventory/hosts.yml playbooks/bezsel-agent.yml --ask-vault-pass
```

This will:

1. Gather service facts.
2. Download `install-agent.sh`.
3. Install the agent (auto-update if enabled).

#### Uninstallation

```
ansible-playbook -i inventory/hosts.yml playbooks/bezsel-agent.yml --tags uninstall_beszel
```

This will:

1. Gather service facts.
2. Download `install-agent.sh`.
3. Run the uninstall command (/tmp/install-agent.sh -u).

#### Related files

* Role: `roles/bezsel/`
* Vault: `inventory/group_vars/beszel_hosts/vault.yml`
* Uninstall Tasks: `roles/bezsel/tasks/uninstall.yml`
* Playbook: `playbooks/bezsel-agent.yml`
