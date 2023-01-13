# AAP TEST

Ansible code to test Ansible Automation Platform functionality.

## Requirements

### Install packages

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

### Copy vars_template.yml

Copy the [vars_template.yml](vars_template.yml) to `vars_aap.ym` and update the variables.

### SSH keypairs

generate ssh-keypairs 

#### SCM credential

Steps:
- generate keypair (make sure these are in the `secrets` directory).
- update `vars_aap.yml` with the key name.

``` yaml
test_aap_git_credential_private_key: "test_id_ed25519"
```

#### Machine credential

Steps:
- generate keypair (make sure these are in the `secrets` directory).
- update `vars_aap.yml` with the key name.
- make sure the ssh public key is added to the `authorized_keys` for the remote test machine.

``` yaml
test_aap_machine_credential_private_key: "test_id_ed25519"
```

## Run tests

``` bash
ansible-playbook -i inventory/hosts -e @vars_aap.yml playbooks/test_aap.yml
```

The [test_aap.yml](playbooks/test_aap.yml) playbook will create components in AAP2.

1. create project
2. create credentials
3. create inventory
4. create jobtemplate
5. run jobtemplate

### variables

See [vars_template.yml](vars_template.yml)
