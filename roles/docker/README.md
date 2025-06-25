Role Name
=========

Docker Role
-----------
This role installs and configures Docker on supported Linux systems. It ensures Docker is installed, running, and that specified users are added to the Docker group.

Requirements
------------
- Supported OS: Debian/Ubuntu
- Ansible 2.9+

Role Variables
--------------
- `docker_group_users`: List of users to add to the Docker group. Default: `["{{ ansible_user }}"]`
- `docker_version`: Version of Docker to install. Default: `latest`
- `docker_apt_repo`: Docker APT repository URL. Default: `https://download.docker.com/linux/{{ ansible_distribution | lower }}`
- `docker_apt_gpg_key`: Docker GPG key URL. Default: `https://download.docker.com/linux/{{ ansible_distribution | lower }}/gpg`

Dependencies
------------
None.

Example Playbook
----------------
    - hosts: servers
      roles:
        - role: docker
          vars:
            docker_group_users:
              - alice
              - bob
            docker_version: latest

License
-------
MIT-0

Author Information
------------------
Your Name <your.email@example.com>

Security Note
-------------
Adding users to the Docker group grants root-level access to the system. Only add trusted users.
