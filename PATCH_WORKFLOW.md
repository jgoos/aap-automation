# Patch Workflow

## Patch Workflow Requirements

- smart inventory
- smtp credentials in `vault.yml`

## Create `vault.yml`

Create a vault file containing the following variables:

| Variable Name        | Description                                                 |
|----------------------|-------------------------------------------------------------|
| vault_workflow_smtp_password | The password for the SMTP authentication for the workflow.  |
| vault_workflow_smtp_email   | The email address used for SMTP authentication for the workflow.  |

Vault example:

``` yaml
vault_workflow_smtp_password: s3cr3tp4ssw0rd
vault_workflow_smtp_email: "johndoe@example.com"

```

## Create Patch Workflow `patch_vars.yml`

Use the `patch_vars_template.yml` template.

1. copy the [patch_vars_template.yml](patch_vars_template.yml) to `patch_vars.yml`
2. fill in the `patch_vars.yml`

> **note:** or add the variables from the template to inventory `group_vars`.

## Usage

Run the [create_patch_workflow.yml](playbooks/create_patch_workflow.yml) playbook to create the workflow.

``` bash
ansible-playbook -e @vault.yml -e @patch_vars.yml playbooks/create_patch_workflow.yml -v --ask-vault-pass
```

## playbooks

| Workflow Step | Playbook |
| --- | --- |
| Playbook to create workflow in AAP | [create_patch_workflow.yml](playbooks/create_patch_workflow.yml) |
| Job Template Sanitize input | [sanitize_input.yml](playbooks/sanitize_input.yml) |
| Job Template Pre-patch reqs and checks | [pre_patching_checks.yml](playbooks/pre_patching_checks.yml) |
| Job Template Patching | [patch_system.yml](playbooks/patch_system.yml) |
| Job Template Reboot system | [reboot_system.yml](playbooks/reboot_system.yml) |
| Job Template Post-patching checks | [post_patching_checks.yml](playbooks/post_patching_checks.yml) |
| Job Template Send email to system owner | [send_email.yml](playbooks/send_email.yml) |

## Workflow Overview

> **note:** This is the version of the workflow without a selection fields for the hosts in the survey.

``` mermaid
graph TB
A[Input] --> B(Sanitize Input)
B --> C(Pre-Patch Checks)
C --> D(Patch)
D --> E(Reboot)
E --> F(Post-Patch Checks)
F --> G(Email System Owner)

subgraph Patch Workflow
A
B
C
D
E
F
G
end

H(Execute Patch Workflow) --> A

```
