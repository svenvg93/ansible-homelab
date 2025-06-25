# Beszel Agent Role

This role installs and manages the Beszel agent for monitoring and management. It is intended for use on all nodes where Beszel should be deployed.

## Features
- Installs or updates the Beszel agent using the official install script
- Configures the agent to use a custom SSH port and key
- Optionally enables auto-update
- Skips installation if the agent is already running (unless forced)

## Requirements
- The variable `beszel_agent_ssh_key` **must** be set in `group_vars/all/vault.yml` or another secure location. This is the SSH key used by the agent.
- Ansible 2.10+

## Role Variables
| Variable                  | Default    | Description                                      |
|---------------------------|------------|--------------------------------------------------|
| `beszel_agent`            | true       | Whether to install the agent                     |
| `beszel_agent_autoupdate` | false      | Enable auto-update for the agent                 |
| `beszel_agent_ssh_port`   | 45876      | SSH port for the agent to use                    |
| `beszel_agent_ssh_key`    | (required) | SSH key for agent, set in Vault or group_vars    |

## Example Playbook
```yaml
- hosts: all
  become: true
  roles:
    - role: beszel-agent
      vars:
        beszel_agent_autoupdate: true
        beszel_agent_ssh_port: 22222
```

## License
MIT-0

## Author
Your Name <your.email@example.com>
