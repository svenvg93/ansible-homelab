# Troubleshooting

Common pitfalls and how to diagnose/fix them.

***

## 1. Inventory Parsing Errors

*   **Symptom:**

    ```
    ERROR! Inventory file is not a valid YAML, JSON, or INI file
    ```
* **Solution:**
  *   Run:

      ```bash
      ansible-inventory --list -i inventory/hosts.yml
      ```

      to get a parse error with line numbers.
  * Ensure correct indentation (2 spaces per level) and valid YAML syntax.

***

## 2. SSH Connection Failures

*   **Symptom:**

    ```
    UNREACHABLE! => {"msg": "Failed to connect to the host via ssh"}
    ```
* **Solution:**
  * Verify SSH key is installed on the target and is not protected by a passphrase (or use an agent).
  * Confirm `ansible_user` or default remote user has `sudo` privileges if needed.
  *   Test manually:

      ```bash
      ssh user@host1.ts.net
      ```

***

## 3. Python Interpreter Not Found

*   **Symptom:**

    ```
    Received: "No module named ansible.module_utils.basic"
    ```
* **Solution:**
  * On the target, ensure Python 3 is installed (`which python3`).
  *   In `group_vars/all.yml`, set:

      ```yaml
      ansible_python_interpreter: /usr/bin/python3
      ```
  * If a host uses a non‐standard interpreter path, set `ansible_python_interpreter` in `host_vars/<host>.yml`.

***

## 4. Role Failures

*   **Symptom:**

    ```
    TASK [roles/docker : Install Docker] … failed with error code 127
    ```
* **Solution:**
  * Check that the APT or YUM repo URLs in `defaults/main.yml` are valid for your distribution.
  * On some distros, you must install prerequisites (e.g., `apt-transport-https`, `ca-certificates`) manually or via a preceding task.
  * Inspect `/var/log/ansible.log` (if enabled) or rerun with `-vvv` for more verbose output.

***

## 5. Service Didn’t Start

*   **Symptom:**

    ```
    TASK [roles/node_exporter : Start Node Exporter] … ok, but service is inactive
    ```
* **Solution:**
  *   SSH into the host and run:

      ```bash
      sudo systemctl status node_exporter
      sudo journalctl -u node_exporter --no-pager
      ```
  * Look for missing binary (perhaps download failed) or permission issues on the service file.
  * Double‐check that `node_exporter_version` was spelled correctly in `group_vars/monitoring_hosts.yml`.

***

## 6. Tailscale Enrollment Issues

*   **Symptom:**

    ```
    TASK [roles/tailscale : tailscale up] … failed with unauthorized key
    ```
* **Solution:**
  * Ensure `tailscale_auth_key` in `group_vars/vpn_hosts.yml` is valid and not expired.
  * On your Tailscale admin panel, generate a new Machine Authorization Key and update the variable.
  * Confirm DNS: if `hosts.yml` uses `host1.ts.net`, make sure the hostname actually resolves (either via Tailscale’s DNS or `/etc/hosts`).

***

## 7. Docker Compose Placeholder Errors

*   **Symptom:**

    ```
    Jinja2 templating error: undefined variable 'some_var'
    ```
* **Solution:**
  * Check that the variable (`some_var`) exists in `group_vars/docker_hosts.yml` or in your `host_vars/`.
  * If you introduced new placeholders in `templates/docker-compose.yml.j2`, be sure to define defaults in `roles/docker/defaults/main.yml`.

***

If you run into other issues, please open an [Issue](https://github.com/svenvg93/ansible-homelab/issues) and include:

* The exact Ansible command you ran
* The full error message (with `-vvv` if possible)
* The relevant snippet of your inventory or group\_vars
