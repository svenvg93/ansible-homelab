# Roles

All roles are housed under the `roles/` directory. Each role is responsible for a discrete piece of functionality. The structure is:

```
roles/
├── docker/
│   ├── defaults/
│   │   └── main.yml
│   ├── tasks/
│   │   └── main.yml
│   ├── handlers/
│   │   └── main.yml
│   └── templates/
│       └── docker-compose.yml.j2
├── node_exporter/
│   ├── defaults/
│   │   └── main.yml
│   ├── tasks/
│   │   └── main.yml
│   ├── handlers/
│   │   └── main.yml
│   └── files/
│       └── node_exporter.service
├── telegraf/
│   ├── defaults/
│   │   └── main.yml
│   ├── tasks/
│   │   └── main.yml
│   ├── handlers/
│   │   └── main.yml
│   └── templates/
│       └── telegraf.conf.j2
└── tailscale/
    ├── defaults/
    │   └── main.yml
    ├── tasks/
    │   └── main.yml
    └── handlers/
        └── main.yml
```

Below is a brief overview of each role:

***

### `roles/docker`

* **`defaults/main.yml`**\
  Contains defaults for `docker_version`, `docker_users`, etc.
* **`tasks/main.yml`**
  1. Adds the Docker APT/GPG repository.
  2. Installs `docker-ce`, `docker-ce-cli`, and `containerd.io`.
  3. Installs `docker-compose` (via package or manual download).
  4. Optionally deploys a templated `docker-compose.yml` from `templates/`.
  5. Adds users in `docker_users` to the `docker` group.
  6. Enables & starts the Docker service.
* **`handlers/main.yml`**
  * Restarts Docker if the repository or configuration changes.

***

### `roles/node_exporter`

* **`defaults/main.yml`**\
  Sets `node_exporter_version` and `node_exporter_port`.
* **`tasks/main.yml`**
  1. Downloads the Node Exporter tarball from GitHub releases.
  2. Extracts the binary into `/usr/local/bin/`.
  3. Installs a systemd service file (from `files/node_exporter.service`).
  4. Enables & starts the `node_exporter` service.
* **`handlers/main.yml`**
  * Restarts or reloads the service if the binary or service file changes.

***

### `roles/telegraf`

* **`defaults/main.yml`**\
  Sets `telegraf_version`, `telegraf_inputs`, and `telegraf_outputs`.
* **`tasks/main.yml`**
  1. Adds the InfluxData APT repository.
  2. Installs `telegraf`.
  3. Deploys `telegraf.conf.j2` from `templates/`, rendering it with the variables declared in `group_vars/monitoring_hosts.yml`.
  4. Enables & starts the Telegraf service.
* **`handlers/main.yml`**
  * Restarts Telegraf whenever the configuration changes.

***

### `roles/tailscale`

* **`defaults/main.yml`**\
  Sets `tailscale_version`, `tailscale_auth_key`, and any `tailscale_extra_args`.
* **`tasks/main.yml`**
  1. Installs Tailscale package (via apt, rpm, or deb as needed).
  2. Runs `tailscale up --authkey={{ tailscale_auth_key }} {{ tailscale_extra_args }}`.
  3. Ensures `tailscaled` is enabled and running.
* **`handlers/main.yml`**
  * Restarts `tailscaled` if the auth key or arguments change.

***

#### Adding New Roles

If you want to add more functionality, simply create a new folder under `roles/`, follow the same subdirectory conventions (`defaults/`, `tasks/`, etc.), and then reference it in one of your playbooks (or create a new playbook). Always document new roles in this file for consistency.
