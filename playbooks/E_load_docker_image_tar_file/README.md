# Ansible Role: Load Docker Images

## Overview
This Ansible role ensures a directory for Docker images exists on the remote server, finds all `.tar` files in that directory, and loads them as Docker images.

## Variables
- `docker_images_dir`: The remote directory containing Docker image `.tar` files (must be defined in `defaults/main.yml` or playbook).

## Tasks Breakdown
- **Ensure docker-images directory exists**: Creates the directory specified by `docker_images_dir` with default permissions, using `become: true` for root access.
- **Get all tar files in the docker-images directory**: Uses `find` to locate all `.tar` files in `docker_images_dir` and registers the results.
- **Load docker images from tar files**: Loads each `.tar` file as a Docker image using the `docker_image` module, extracting the image name from the file's basename (removing `.tar`). Includes a 300-second timeout and fails only if the "Loaded image:" message is absent in the output.

## Usage Tips
- Define `docker_images_dir` in `defaults/main.yml` or playbook. Example:
  ```yaml
  docker_images_dir: "/home/{{ ansible_user }}/docker-images"