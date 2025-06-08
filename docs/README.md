---
description: >-
  Overview of the Ansible Homelab Automation repository, goals, and quick start
  guide.
---

# Introduction

This repository automates the configuration and management of a personal homelab using [Ansible](https://www.ansible.com/). Its primary goals:

* Install and configure Docker
* Bootstrap: provision new machines with timezone, locale, user setup, SSH hardening, firewall, and base packages
* Docker: install and configure Docker Engine and Docker Compose
* VPN: enroll hosts in Tailscale for secure mesh VPN networking
* Speedtest:  Ookla speedtests CLI
* Beszel: install or uninstall the Beszel agent for remote monitoring with auto-update support
* Maintenance: perform system updates, log cleanup, Docker pruning, and journal vacuum tasks

***

## Quick Start

1.  Clone the repository:

    ```bash
    git clone https://github.com/svenvg93/ansible-homelab.git
    cd ansible-homelab
    ```
2.  Install required Python packages on your control node (Python 3.6+):

    ```bash
    pip3 install -r requirements.txt
    ```
3. Create or adjust `inventory/hosts.yml` with your target hosts.
4. Review and customize group variables under `group_vars/`.
5.  Run the playbooks:

    ```bash
    ansible-playbook -i inventory/hosts.yml playbooks/site.yml
    ```

For more details, see [Requirements](requirements.md) and [Setup & Configuration](broken-reference).
