# Ansible Learning

A collection of Ansible playbooks and role-based labs for practicing server
configuration, web-server deployment, user management, templates, handlers,
loops, variables, and Ansible Vault.

The examples are independent. Choose the directory that matches the concept
you want to practice, review its inventory and variables, and run its
playbook from that directory.

## Repository layout

| Directory | Topics |
| --- | --- |
| `ansible-lab/` | Progressive labs covering facts, variables, loops, handlers, roles, users, and Nginx |
| `local-machine/` | Role-based web-server setup for a local inventory |
| `multi-user/` | Cross-platform user creation with Debian and Red Hat variables |
| `ansible-template/` | An Apache role and Jinja2 templating |
| `webserver-setup/` | OS-specific Nginx configuration with host variables |
| `apache-setup/` | Basic Apache installation examples |
| `database-setup/` | Database setup example using encrypted variables |
| `ansibile-learn/` | Additional introductory playbook exercises |
| `ansible-crontab/` | Scheduled backup configuration |
| `single-server-ansible/` | Single-server Apache example |
| `multi-server-ansible/` | Ansible configuration for a multi-server exercise |

Most directories contain their own `ansible.cfg`, inventory, playbook, and
supporting roles or templates. The role directories also include Ansible role
metadata, handlers, defaults, variables, and (where applicable) basic tests.

## Requirements

- Ansible Core installed on the control machine
- SSH access to the hosts listed in the selected inventory
- A user with `sudo` privileges when a playbook uses `become: true`
- Python available on managed hosts
- `community.general` for examples that use the UFW module

Install the community collection when needed:

```bash
ansible-galaxy collection install community.general
```

## Quick start

1. Change into an example directory.
2. Edit `hosts.ini` or `inventory/hosts.ini` for your machines.
3. Review variables and templates before running the playbook.
4. Validate connectivity.
5. Run the playbook.

```bash
cd local-machine
ansible all -i inventory/hosts.ini -m ping
ansible-playbook -i inventory/hosts.ini site.yml --ask-become-pass
```

For a role-based example with a top-level inventory:

```bash
cd webserver-setup
ansible all -i hosts.ini -m ping
ansible-playbook -i hosts.ini play.yml --ask-become-pass
```

Use `--check` to preview changes where supported:

```bash
ansible-playbook -i hosts.ini play.yml --check --diff
```

## Ansible Vault

Some examples contain vault-backed variables, including
`database-setup/vars/vault.yml` and the vault exercise under
`ansible-lab/lab-4/`. Keep vault passwords and decrypted secrets out of Git.
The repository ignores common vault password files.

Run a playbook with a prompted vault password:

```bash
ansible-playbook -i hosts.ini setup_db.yml --ask-vault-pass
```

You can inspect an encrypted file with:

```bash
ansible-vault view vars/vault.yml
```

## Notes

- Inventory host groups must match the `hosts:` value in each playbook.
- Paths and package names may need adjustment for the target operating system.
- Review firewall, service, and user changes before applying examples to
  production systems.
