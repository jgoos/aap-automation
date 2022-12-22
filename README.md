# aap2-automation

This repository contains ansible code to automate tasks in Ansible Automation Platform 2.
Tested with AAP2 version: *2.3*

## requirements


### install packages

Install requirements on ansible control host.
This is a RHEL8 or RHEL9  system with ansible-core. 

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

ansible-galaxy install -r collections/requirements.yml

```

### create tower_cli.cfg

Follow the instructions in the documentation to create the `tower_cli.cfg` file.

See: https://console.redhat.com/ansible/automation-hub/repo/published/ansible/controller/docs/

- get a oauth token
- create the `~/.tower_cli.cfg` 

``` shell

awx login -k --conf.host https://<AAP_CONTROLLER_FQDN> --conf.username <USER_NAME> --conf.password <PASSWORD>

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
