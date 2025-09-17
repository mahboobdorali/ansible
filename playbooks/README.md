# Ansible Playbook

## Execution Instructions
To run this playbook on all hosts in the `dummy` group:  
`ansible-playbook -i inventory.ini [name-of-paly-book].yaml`

To run on a specific server from the `dummy` group (e.g., `****`):  
`ansible-playbook -i inventory.ini [name-of-play-book].yaml --limit [server_name_on_dummy]`

example: `ansible-playbook playbooks/playbook.yml -i inventory.ini --limit [server_name_on_dummy]`

pass -K for get sudo password
if not have any ssh key, use with --ask-pass argument
