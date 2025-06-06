# Contributing

Thank you for considering contributing to **ansible-homelab**! Whether it’s a bug fix, new role, or improved documentation, your help is welcome.

***

## How to Contribute

1. **Fork the repository**\
   Click “Fork” in the top‐right of the GitHub page to create your own copy.
2.  **Create a new branch**

    ```bash
    git checkout -b feature/my-feature
    ```
3. **Make your changes**
   * Follow the same directory layout for roles and playbooks.
   * If adding a new role, document it under Roles and link from `SUMMARY.md`.
   * If fixing documentation, update the relevant `.md` file in this docs set.
4. **Test your changes**
   * Run lint checks (e.g., `ansible-lint` on playbooks).
   * Apply the playbook on a non-production machine (e.g., a disposable VM or local VM).
5. **Submit a Pull Request**\
   Push your branch to your fork, then open a PR against `svenvg93/ansible-homelab:master`.
   * Fill in the PR template with description, motivated changes, and any backward‐compatibility notes.
   * Tag maintainers if you need a review or have questions (e.g., `@svenvg93`).

***

## Coding Standards

* Use **YAML** best practices (two‐space indentation, lowercase keys with underscores).
* Role names should be short and expressive (e.g., `monitoring` rather than `install_monitoring_agents`).
* Variables: use descriptive names, avoid reserved words. Provide sensible defaults in `defaults/main.yml`.
* Templates: keep Jinja2 logic minimal—complex logic should live in a `vars` file or in a role’s `defaults/`.

***

## License

By contributing, you agree that your changes will be licensed under the existing MIT License. If you add new code, please choose a compatible license and include a header in new files.
