# Bootstrap Role

This role prepares a new machine with essential system settings and packages. It is intended to be run as the first step when deploying a new server.

## Features
- Set system timezone and locale
- Install essential packages
- Upgrade all packages
- Enable automatic security updates
- Configure unattended-upgrades notification
- Harden SSH by disabling root login

## Role Variables

| Variable                      | Default                | Description                                      |
|-------------------------------|------------------------|--------------------------------------------------|
| `bootstrap_timezone`          | Europe/Amsterdam       | System timezone to set                           |
| `bootstrap_locale`            | en_US.UTF-8            | System locale to generate and set                 |
| `bootstrap_essential_packages`| [unattended-upgrades, tcpdump] | List of essential packages to install   |
| `bootstrap_unattended_mail`   | root                   | Email for unattended-upgrades notifications       |

## Example Playbook

```yaml
- hosts: new_servers
  become: true
  roles:
    - role: bootstrap
      vars:
        bootstrap_timezone: Europe/Berlin
        bootstrap_locale: en_GB.UTF-8
        bootstrap_essential_packages:
          - unattended-upgrades
          - curl
          - vim
        bootstrap_unattended_mail: admin@example.com
```

## License
MIT-0

## Author
Your Name <your.email@example.com> 