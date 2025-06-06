# Introduction

This repository automates the configuration and management of a personal homelab using [Ansible](https://www.ansible.com/). Its primary goals:

* Install and configure Docker
* Deploy Node Exporter for Prometheus metrics
* Enroll machines in Tailscale VPN
* Install and configure Telegraf monitoring agent
* Perform routine system maintenance tasks
* Set timezone and basic system parameters

By the end of this guide, you’ll know how to:

1. Prepare your control node and target hosts
2. Structure inventory and variable files
3. Run individual playbooks or the full site
4. Customize roles and playbooks to your own needs

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

For more details, see [Requirements](requirements.md) and [Setup & Configuration](setup.md).
