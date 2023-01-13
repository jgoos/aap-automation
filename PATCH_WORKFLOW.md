# Patch Workflow


## Overview

``` mermaid
graph LR
A[Input] --> B(Sanitize Input)
B --> C(Pre-Patch Checks)
C --> D(Patch)
D --> E(Reboot)
E --> F(Post-Patch Checks)
F --> G(Email System Owner)
```

