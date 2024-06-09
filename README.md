# Ansible Collection - mikejonesey.fluxcd

Collection of roles for automating manual tasks getting started with flux. Once flux is installed and bootsrapped all other tasks can be easily maintained and copied between envs with git/sed.

tasks:
- installing common cli tools flux,kustomize,helm
- initial bootstrap
- create secrets

# Top Level Playbook Examples

note, if you use the var "playbook_dir" in playbook_dir/group_vars, 
then you'll need to copy the playbook contents as opposed to importing the playbook 
(ansible does currently change playbook_dir on playbook import to the collection directory, there is a bug report open). 

## Cli Tools

```
- hosts: localhost
  tasks:
    - ansible.builtin.debug:
        msg: FLUXCD CLI

- name: Include playbook from fluxcd collection
  ansible.builtin.import_playbook: mikejonesey.fluxcd.fluxcd_cli_tools
```

## Main Playbook (bootstrap+secrets)

```
- hosts: localhost
  tasks:
    - ansible.builtin.debug:
        msg: FLUXCD

- name: Include playbook from fluxcd collection
  ansible.builtin.import_playbook: mikejonesey.fluxcd.fluxcd

```