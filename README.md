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

| Variable | Default | Description |
|---|---|---|
| `scaffold_message` | `"Hello from the scaffold role"` | Message written to the config file |

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
