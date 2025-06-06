# Files Directory

Any static files that need to be copied to remote hosts should go under `files/`. The structure is:

```
files/
├── docker/
│   └── docker-compose.yml.j2
├── telegraf/
│   └── telegraf.conf.j2
└── other/
    └── custom_script.sh
```

*   **`docker/docker-compose.yml.j2`**\
    A Jinja2‐templated Compose file used to spin up your most‐used Docker services.\
    Example:

    ```yaml
    version: '3.8'
    services:
      nginx:
        image: nginx:latest
        ports:
          - "80:80"
        restart: always
    ```

    Any Jinja2 placeholders (e.g. `{{ some_var }}`) should match variables defined in `group_vars/docker_hosts.yml` or `host_vars/`.
* **`telegraf/telegraf.conf.j2`**\
  The base Telegraf configuration that uses variables from `group_vars/monitoring_hosts.yml`.\
  You can customize input and output plugins here.
*   Other subfolders (e.g., `other/`) can contain miscellaneous scripts or configuration snippets. Roles should reference these paths explicitly; e.g.:

    ```yaml
    - name: Copy custom script
      template:
        src: files/other/custom_script.sh
        dest: /usr/local/bin/custom_script.sh
        mode: '0755'
    ```

> **Tip:** Always use `template:` (not `copy:`) when using `.j2` files so that variables get rendered correctly.
