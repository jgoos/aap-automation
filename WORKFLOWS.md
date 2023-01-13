# WORKFLOWS


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

## Initial

# Automation Org
- Create inventory
- Create inventory_source
- Create job_templates

# Specific Org
- Create smart inventory
- Read current smart inventory and update variable for hosts.
- Update WF (using updated variable for hosts).
  - using job_templates from automation Org

## Update

- Read current (smart)inventory and update variable for hosts.
- Update WF (using updated variable for hosts).
  
