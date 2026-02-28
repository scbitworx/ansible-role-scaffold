# Scaffold Role

Trivial Ansible role used as a reference template for all future roles in the
`scbitworx` organization. It validates the full toolchain end-to-end: variable
loading, package installation, template deployment, handler notification,
Molecule testing, and GitHub Actions CI.

## What It Does

- Installs `tree` via the distro package manager
- Deploys a trivial config file to `/etc/scaffold_example.conf`
- Notifies a handler to confirm template deployment

## Supported Platforms

- Arch Linux
- Ubuntu 24.04
- Debian 12

## Role Variables

| Variable           | Default                          | Description                        |
| ------------------ | -------------------------------- | ---------------------------------- |
| `scaffold_message` | `"Hello from the scaffold role"` | Message written to the config file |

## Using This as a Template

To create a new role from this scaffold:

1. Copy the repo and rename to `ansible-role-<your_role_name>`
2. Update `meta/main.yml`: set `role_name` to your role name
3. Rename all variables: `scaffold_` → `<your_role_name>_` (public),
   `__scaffold_` → `__<your_role_name>_` (private in `vars/`)
4. Rename handlers: `Scaffold |` → `<Your_role_name |>`
5. Update `.ansible-lint` `extra_vars` to mock your role's variables
6. Replace the trivial package/template tasks with real work
7. Update `molecule/default/converge.yml` and `verify.yml` for your role
8. Update this README

## Testing

### Prerequisites

- Python 3 + pip
- Docker (running)
- Install the toolchain:

```bash
pip install ansible-core ansible-lint yamllint molecule molecule-plugins[docker]
ansible-galaxy collection install community.general
```

### Lint (fast — run before every commit)

```bash
yamllint .
ansible-lint
```

### Molecule (full integration test)

```bash
# Run full test suite (lint + converge + verify + destroy)
molecule test

# Converge and keep containers running for debugging
molecule converge
molecule login -h archlinux
molecule verify
molecule destroy
```

## License

MIT
