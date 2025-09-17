## Ansible Configuration (`ansible.cfg`)

The `ansible.cfg` file defines default settings for running Ansible commands and playbooks.
In this project, it is used to:

- **Set the default inventory file** (`inventory = ./inventory.ini`) so you don’t need to specify `-i` every time.
- **Disable host key checking** (`host_key_checking = False`) to prevent SSH fingerprint prompts during automation.
- **Disable retry files** (`retry_files_enabled = False`) to avoid creating unnecessary `.retry` files.
- **Define the roles path** (`roles_path = ./playbooks/roles`) so Ansible can find roles without extra configuration.

With these settings, running `ansible-playbook` is simpler and requires fewer command-line options.


# inventory.ini file

## Overview
This Ansible inventory file organizes servers into two groups: `production` for live servers with connection details and `dummy` for placeholder/test hosts.

## Structure
- **[production]**: Live servers with IP addresses and SSH users.
    - `*** ansible_host=**.**.***.*** ansible_user=****`: Host alias `s249`, connects to IP `**.**.***.***` with user `*****`.
- **[dummy]**: Placeholder hosts without connection details.
    - `****`: Host aliases, unresolved unless defined elsewhere.

## Usage
- Use with: `ansible -i inventory.ini <group> -m <module>`.
- Example: `ansible -i inventory.ini production -m ping` to test production hosts.
- Keep sensitive data out; use Ansible Vault if needed.
