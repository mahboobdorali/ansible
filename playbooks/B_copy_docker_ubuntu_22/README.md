# Ansible Role: Copy Docker Files

## Overview
This Ansible role ensures a target directory exists on the remote server and copies specified Docker `.deb` files from the control node to the remote server if they are missing.

## Variables
- `target_dir`: The remote directory where Docker files will be stored (must be defined in `defaults/main.yml` or playbook).
- `docker_files`: A list of Docker `.deb` file names to check and copy (must be defined in `defaults/main.yml` or playbook).

## Tasks Breakdown
- **Ensure target directory exists**: Creates the directory specified by `target_dir` with permissions `0755`.
- **Check if Docker files exist on remote server**: Uses `stat` to check if each file in `docker_files` exists on the remote server.
- **Copy missing Docker deb files from control node**: Copies files from the control node to `target_dir` if they don’t exist, with permissions `0644`.

## Usage Tips
- Define `target_dir` and `docker_files` in `defaults/main.yml` or playbook. Example:
  ```yaml
  target_dir: "/home/{{ ansible_user }}/install/docker-files"
  docker_files:
    - docker-ce.deb
    - docker-compose-plugin.deb