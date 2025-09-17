# Ansible Role: Configure Docker Group

## Overview
This Ansible role ensures the `docker` group exists on the remote server, adds the current user to the `docker` group, and notifies the user to re-login for group changes to take effect.

## Variables
- `ansible_user`: The remote user to be added to the `docker` group (dynamically set per host).

## Tasks Breakdown
- **Ensure docker group exists**: Creates the `docker` group if it does not exist.
- **Add current user to docker group**: Adds the user specified by `ansible_user` to the `docker` group, appending to existing groups.
- **Notify user to re-login for docker group changes**: Outputs a debug message reminding the user to log out and back in (or restart their SSH session) to apply group changes.

## Usage Tips
- Assumes Docker is installed on the target server, as the `docker` group is typically used for Docker access.
- Requires `become: true` for group and user modifications, as these operations need root privileges.
- Ensure SSH access to target hosts is configured in the inventory.
- After running, users must re-login or restart their SSH session for group membership to take effect.