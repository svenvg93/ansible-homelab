# Tailscale Role

This role installs and configures Tailscale on a host, including authentication and optional SSH enablement.

## Features
- Installs Tailscale using the official install script
- Authenticates with Tailscale using an auth key (stored in Vault)
- Optionally enables Tailscale SSH
- Ensures the service is enabled and running

## Requirements
- The variable `tailscale_auth_key` **must** be set in `group_vars/all/vault.yml` or another secure location. This is the Tailscale auth key for joining the network.
- Ansible 2.10+

## Role Variables
| Variable                | Default                        | Description                                      |
|-------------------------|--------------------------------|--------------------------------------------------|
| `tailscale_enable_ssh`  | true                           | Whether to enable Tailscale SSH                  |
| `tailscale_install_url` | https://tailscale.com/install.sh | URL for the Tailscale install script           |
| `tailscale_auth_key`    | (required)                     | Auth key for Tailscale, set in Vault or group_vars |

## Example Playbook
```yaml
- hosts: all
  become: true
  roles:
    - role: tailscale
      vars:
        tailscale_enable_ssh: true
```

## Security Note
Store your `tailscale_auth_key` securely in Ansible Vault. Never commit secrets to version control.

## License
MIT-0

## Author
Your Name <your.email@example.com> 