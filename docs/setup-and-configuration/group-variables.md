# Group Variables

All default variables for your playbooks and roles live in the `group_vars/` directory, mirrored under your inventory folder:

```
inventory/
└── group_vars/
    ├── beszel_hosts/
    │   └── vault.yml      # vaulted SSH key for Beszel Agent
    └── tailscale_hosts/
        └── vault.yml      # vaulted auth key for Tailscale
```

## Vaulted group vars

- **`inventory/group_vars/beszel_hosts/vault.yml`**  
  Contains the encrypted SSH key for the Beszel agent:
  ```yaml
  beszel_agent_ssh_key: "ssh-ed25519 AAAA…"
  ```
- **`inventory/group_vars/tailscale_hosts/vault.yml`**  
  Contains the encrypted Tailscale auth key:
  ```yaml
  tailscale_auth_key: "tskey-XXXXXXXXXXXXXXXX"
  ```

> **Tip:** Use `ansible-vault edit` or `ansible-vault create` to manage these sensitive files.

