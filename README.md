# Ansible Collection - mikejonesey.fluxcd

Collection of roles for automating manual tasks getting started with flux. Once flux is installed and bootsrapped all other tasks can be easily maintained and copied between envs with git/sed.

collection tasks:
- installing common cli tools
- initial bootstrap
- create secrets
- uninstall fluxcd

# Installation

```
ansible-galaxy collection install mikejonesey.fluxcd
```

# Top Level Playbook Examples

The following are examples of the plays being included in top level playbooks.

## Cli Tools

installs:
- flux
- kustomize
- helm

```
- hosts: localhost
  tasks:
    - ansible.builtin.debug:
        msg: FLUXCD CLI

- name: Include playbook from fluxcd collection
  ansible.builtin.import_playbook: mikejonesey.fluxcd.fluxcd_cli_tools
```

## Main Playbook

- Bootstrap FluxCD
- Flux secrets
  - git repository auth
  - helm repository auth
  - docker repository auth
- Kubernetes generic/opaque secrets
  - incoming webhook secret
  - outgoing notification provider secrets

```
- hosts: localhost
  tasks:
    - ansible.builtin.debug:
        msg: FLUXCD

- name: Include playbook from fluxcd collection
  ansible.builtin.import_playbook: mikejonesey.fluxcd.fluxcd_setup

```
###Warning

if you use the var "playbook_dir" in playbook_dir/group_vars, 
then you'll need to copy the playbook contents as opposed to importing the playbook 
(ansible does currently change playbook_dir on playbook import to the collection directory, there is a bug report open). 

(this can effect secrets defined in group_vars/host_vars using playbook_dir in the path to say passwordstore)

in this case, just copy or symbolic link a playbook to top level.

## Uninstall Playbook

This is useful when migrating to a new git repo, if you are just changing an option using the same git ref then re-run bootstrap instead.

```
- hosts: localhost
  tasks:
    - ansible.builtin.debug:
        msg: FLUXCD

- name: Include playbook from fluxcd collection
  ansible.builtin.import_playbook: mikejonesey.fluxcd.fluxcd_setup

```
