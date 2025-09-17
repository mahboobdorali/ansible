# Ansible Role: Install Docker Packages

## Overview
This Ansible role ensures a target directory exists on the remote server and installs Docker `.deb` packages from that directory using the `apt` module.

## Variables
- `target_dir`: The remote directory containing Docker `.deb` files (must be defined in `defaults/main.yml` or playbook).
- `docker_files`: A list of Docker `.deb` file names to install (must be defined in `defaults/main.yml` or playbook).

## Tasks Breakdown
- **Ensure target directory exists**: Creates the directory specified by `target_dir` with permissions `0755`.
- **Install all docker deb files in target directory**: Installs each `.deb` file listed in `docker_files` using `apt`.

## Usage Tips
- Define `target_dir` and `docker_files` in `defaults/main.yml` or playbook. Example:
  ```yaml
  target_dir: "/home/{{ ansible_user }}/install/docker-files"
  docker_files:
    - docker-ce.deb
    - docker-compose-plugin.deb