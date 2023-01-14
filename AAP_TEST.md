# AAP TEST

Ansible code to test Ansible Automation Platform functionality.

## Requirements

### Copy vars_template.yml

Copy the [vars_template.yml](vars_template.yml) to `vars_aap.ym` and update the variables.

#### Variables

| Variable Name                           | Example Value          |
|-----------------------------------------|------------------------|
| test_aap_git_credential_name            | "test_git_cred"        |
| test_aap_git_credential_private_key     | "test_id_ed25519"      |
| test_aap_git_url                        | "<GIT_REPO_URL>"       |
| test_aap_git_user                       | "<GIT_USER>"           |
| test_aap_organization_name              | "Test"                 |
| test_aap_project_description            | "AAP tests"            |
| test_aap_project_name                   | "test_project"         |
| test_aap_machine_credential_name        | "test_machine_cred"    |
| test_aap_machine_user                   | "<REMOTE_USER>"        |
| test_aap_machine_credential_private_key | "test_id_ed25519"      |

### SSH keypairs

Generate ssh-keypairs 

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
