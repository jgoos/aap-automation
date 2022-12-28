# WORKFLOWS

## Patch Workflow

### Credentials

email:

- password
- smtp server
- email address

### Variables

- input choices
- pre-patch choices
- patch choices
- reboot choices
  - direct
  - write facts in inventory
- post-patch choices
- email and message choices

### Playbooks

- [ ] Playbook to create workflow in AAP
- [ ] Job Template Sanitize input
- [ ] Job Template Pre-patch reqs and checks
- [ ] Job Template Patching
- [ ] Job Template Reboot system
- [ ] Job Template Post-patching checks
- [ ] Job Template Send email to system owner

### Overview

```mermaid
graph TB
    input -->|On Success| sanitize["Sanitize input"]
    sanitize["Sanitize input"] -->|On Success| pre-patch["Pre-patch"]
    pre-patch["Pre-patch"] -->|On Success| patching["Patching"]
    patching["Patching"] -->|On Success| reboot["Reboot"]
    reboot["Reboot"] -->|On Success| post-patch["Post-patch"]
    post-patch["Post-patch"] -->|On Success| send-email["Send email to system owner"]

    input -->|On Failure| error["Raise Error"]
    sanitize -->|On Failure| error
    pre-patch -->|On Failure| error
    patching -->|On Failure| error
    reboot -->|On Failure| error
    post-patch -->|On Failure| error
```
