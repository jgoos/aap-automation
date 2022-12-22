# aap2-automation

This repository contains ansible code to automate tasks in Ansible Automation Platform 2.  
Tested with AAP2 version: **2.3**

## requirements


### install packages

Install requirements on the ansible control host.
This is a RHEL8 or RHEL9 system with ansible-core. 

on RHEL8:
``` shell
sudo subscription-manager repos --enable ansible-automation-platform-2.3-for-rhel-8-x86_64-rpms
```

on RHEL9:
``` shell
sudo subscription-manager repos --enable ansible-automation-platform-2.3-for-rhel-9-x86_64-rpms
```

``` shell
sudo dnf install -y automation-controller-cli.x86_64
```

### install ansible collections

``` shell
ansible-galaxy collection install ansible.controller
```

### create tower_cli.cfg

Follow the instructions in the documentation to create the `tower_cli.cfg` file.

See: https://console.redhat.com/ansible/automation-hub/repo/published/ansible/controller/docs/

- get a oauth token

``` shell

awx login -k --conf.host https://<AAP_CONTROLLER_FQDN> --conf.username <USER_NAME> --conf.password <PASSWORD>

```
- create the `~/.tower_cli.cfg` 

``` ini
[general]
host = https://<AAP_CONTROLLER_FQDN>
verify_ssl = true
oauth_token = <TOKEN_FROM_PREVIOUS_STEP>
```

## monitoring

## tests

### create content

1. create credential
2. create project
3. create inventory
4. create jobtemplate

### execute

1. execute jobtemplate


## variables

Create group vars `group_vars/all.yml`

``` yaml
test_aap_git_credential_name: "test_git_cred"
test_aap_git_url: <GIT_REPO_URL>
test_aap_git_user: "<GIT_USER>"
test_aap_organization_name: "Test"
test_aap_project_description: "AAP2 tests"
test_aap_project_name: "test_project"
test_aap_machine_credential_name: "test_machine_cred"
test_aap_machine_user: "cloud-user"
```

## run

``` shell
ansible-playbook test_aap.yml
```
