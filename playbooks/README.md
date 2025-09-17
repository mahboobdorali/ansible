# Ansible Playbook

## Execution Instructions
To run this playbook on all hosts in the `dummy` group:  
`ansible-playbook -i inventory.ini [name-of-paly-book].yaml`

To run on a specific server from the `dummy` group (e.g., `****`):  
`ansible-playbook -i inventory.ini [name-of-play-book].yaml --limit [server_name_on_dummy]`

example: `ansible-playbook playbooks/playbook.yml -i inventory.ini --limit [server_name_on_dummy]`

pass -K for get sudo password
if not have any ssh key, use with --ask-pass argument

========================================================================
# Setup SSH Keys Playbook
## Overview
This playbook sets up SSH keys on remote servers in the `dummy` group. It ensures an SSH key pair exists locally, then copies the public key to the remote server's `authorized_keys` for passwordless access.

## Variables
- `ssh_key_path`: Path to local SSH key (defaults to `~/.ssh/id_rsa`).
- `ssh_user`: Remote user (uses `ansible_user`).

## Tasks Breakdown
- **Ensure ~/.ssh directory exists on remote**: Creates `/home/{{ ssh_user }}/.ssh` with proper permissions.
- **Generate SSH key pair on control machine if not exists**: Runs locally to create RSA key pair (4096 bits) if missing.
- **Read public key content (only if exists)**: Slurps the public key file locally.
- **Add public key to authorized_keys on remote**: Appends the public key to remote `authorized_keys` if available.

## Usage Tips
- Assumes inventory file with `dummy` group defined.
- Run with appropriate privileges; no `become: true` for remote tasks.
- Verify key paths and users before execution.

========================================================================
