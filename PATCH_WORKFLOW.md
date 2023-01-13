# Patch Workflow


## Overview


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