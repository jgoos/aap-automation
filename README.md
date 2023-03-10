# Ansible Automation

Create objects in Ansible Automation Platform.

## Patch Workflow

- [PATCH_WORKFLOW.md](PATCH_WORKFLOW.md)

## Test Ansible Automation Platform:

- [AAP_TEST.md](AAP_TEST.md)


## Requirements

Install requirements on the ansible control host.
This is a RHEL8 or RHEL9 system with ansible-core. 

on RHEL8:
``` bash
sudo subscription-manager repos --enable ansible-automation-platform-2.3-for-rhel-8-x86_64-rpms
sudo dnf install -y automation-controller-cli.x86_64
```

on RHEL9:
``` bash
sudo subscription-manager repos --enable ansible-automation-platform-2.3-for-rhel-9-x86_64-rpms
sudo dnf install -y automation-controller-cli.x86_64
```

### Create Project in Ansible Automation Platform

Create a SCM project in `AAP` using this git repository as source.

See: https://docs.ansible.com/automation-controller/latest/html/quickstart/create_project.html

> **note:** Use the same project and organization as defined in the `patch_vars.yml` (which is based on [patch_vars_template.yml](patch_vars_template.yml).

### Install ansible collections

``` bash
ansible-galaxy collection install ansible.controller
```

### Create tower_cli.cfg

Follow the instructions in the documentation to create the `tower_cli.cfg` file.

See: https://console.redhat.com/ansible/automation-hub/repo/published/ansible/controller/docs/

- get a oauth token

``` bash

awx login -k --conf.host https://<AAP_CONTROLLER_FQDN> --conf.username <USER_NAME> --conf.password <PASSWORD>

```
- create the `~/.tower_cli.cfg` 

``` ini
[general]
host = https://<AAP_CONTROLLER_FQDN>
verify_ssl = true
oauth_token = <TOKEN_FROM_PREVIOUS_STEP>
```
