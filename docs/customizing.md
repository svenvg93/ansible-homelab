# Customizing

This section explains how to override or extend defaults to tailor the automation to your own homelab.

***

## Overriding Defaults

1.  **Per‐Group Overrides**\
    Edit the relevant `group_vars/<group>.yml` to change default variables. For example, to force Telegraf to send metrics to a different URL:

    ```yaml
    # group_vars/monitoring_hosts.yml
    telegraf_outputs:
      - name: "influxdb"
        url: "http://my-influx.example:8086"
    ```
2.  **Per‐Host Overrides**\
    Create a `host_vars/<hostname>.yml` file and set host-specific values. Example:

    ```yaml
    # host_vars/host3.ts.net.yml
    timezone: "America/New_York"
    node_exporter_port: 9200
    ```
3.  **Environment Variables**\
    You can also pass extra vars at runtime:

    ```bash
    ansible-playbook -i inventory/hosts.yml playbooks/site.yml      --extra-vars "install_telegraf=false"
    ```

***

## Adding New Playbooks

If you have a new use case (e.g., “backup”), follow these steps:

1.  Create `playbooks/backup.yml`:

    ```yaml
    ---
    - name: Run backups on backup_hosts
      hosts: backup_hosts
      become: true
      roles:
        - role: roles/backup
    ```
2. Add a `roles/backup/` directory (defaults, tasks, handlers, etc.).
3. Define variables in `group_vars/backup_hosts.yml`.
4. Add an entry in `SUMMARY.md` and create `backup.md` for documentation.

***

## Templating Tips

*   Use Jinja2 tests/filters in your `.j2` files. Example in `telegraf.conf.j2`:

    ```jinja
    [[outputs.influxdb_v2]]
      urls = ["{{ telegraf_outputs[0].url }}"]
      token = "{{ telegraf_outputs[0].token }}"
      bucket = "{{ telegraf_outputs[0].bucket }}"
      organization = "{{ telegraf_outputs[0].organization }}"
    ```
* Use `lookup('file', 'path/to/file')` if you need to inject certificate files or static text.
* Remember to always call `template:` (not `copy:`) for files ending in `.j2`.

***

## Renaming Groups

If you rename any inventory group, update:

* `group_vars/<new_group_name>.yml`
* All playbooks referencing that group (e.g., `- hosts: <new_group_name>`).
* Any role dependencies or conditionals using the old group name.

***

## Extending Roles

To extend a role without modifying the original, use role dependency or role overriding in your playbook:

```yaml
roles:
  - role: roles/docker
    tags: install_docker
  - role: my_custom_docker_tweak
    when: "ansible_distribution == 'Ubuntu'"
```

This runs `roles/docker` first and then runs `my_custom_docker_tweak` only on Ubuntu hosts.
