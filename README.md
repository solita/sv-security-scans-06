# 2023-02-18

## Why Semgrep is Needed?

1. GitHub provides CodeQL SAST scans for **public** repos for free.

2. But if your organization does not have GHAS (GitHub Advanced 
   Security license), CodeQL scans are **not** available for your 
   **private** and **internal** repos.

3. This is where Semgrep comes in. It contains a free SAST tier
   covering numerous languages. You can use it in your private
   and internal repos.

4. Semgrep is a powerful static analysis tool with rich sets of 
   default and custom rules: https://semgrep.dev/

## Contents of this repo

In
```
.github/workflows
```
we provide a few sample workflows which you will easily adjust
for your needs.