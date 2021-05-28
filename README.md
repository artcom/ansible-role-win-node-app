# Node App
Ansible role to clone a Node app and install its dependencies on a Windows 10 machine.

## Description
This role will clone a node app from a git repository over https, install Node and the Node app dependencies. Credentials can be passed to the role to install from a private repository. Optionally Node gyp dependencies will be installed.

## Requirements
This role requires a reboot handler.

## Role Variables
Available variables are listed below, along with default values `(see defaults/main.yml)`:
```yaml
node_version: null
node_app_path: null
node_app_repo: null
node_app_tag: null
use_node_gyp: false
python2_version: null
visual_cpp_build_tools_version: null
```
Required variables (role will fail if the variables are not set):
```yaml
node_version: "string"
node_app_path: "string"
node_app_repo:
  url: "string"
  private: "boolean"
node_app_tag: "string"
```
Required variables for a private repo (role will fail if the variables are not set):
```yaml
deployment_user: "string"
deployment_password: "string"
```
Required variables when using node_gyp (role will fail if the variables are not set):
```yaml
python2_version: "string"
visual_cpp_build_tools_version: "string"
```

## Dependencies
* [check-required-variables](https://github.com/artcom/ansible-role-check-required-variables)

# Example Playbook
```yaml
- name: install node app
  hosts: all
  handlers:
    - name: reboot
      win_reboot:

  tasks:
    - ansible.builtin.include_role:
        name: win-node-app
      vars:
        node_version: "14.4.0"
        node_app_path: "{{ ansible_user_dir }}/node_app_name"
        node_app_repo:
          url: "https://github.com/username/node_app_name.git"
        node_app_tag: "1.0.0"
```

## License
MIT
