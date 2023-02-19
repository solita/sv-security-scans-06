# 2023-02-18

## Why Semgrep SAST is Needed?

1. GitHub provides CodeQL SAST (Static Application Security Test) 
   scans for **public** repos for free.

2. But if your organization does not have GHAS (GitHub Advanced 
   Security license), CodeQL scans are **NOT** available for your 
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

```
.github
└── workflows
    ├── semgrep-01.yml
    └── semgrep-02.yml
```

### 


## Remarks

1. Even though Semgrep is capable to generate `.sarif`
   (Static Analysis Results Interchange Format, 
   https://sarifweb.azurewebsites.net/) files, which you can 
   upload to GitHub and browse their nice representation there,
2. The action `github/codeql-action/upload-sarif@v2`
   you need to upload `.sarif` files requires that you have
   GHAS (GitHub Advanced Security license). This is a catch:
   Semgrep (no GHAS needed) generates a desired `.sarif`,
   but you cannot upload it to GitHub (requires GHAS).
3. You may find useful Python command line tools 
   https://github.com/microsoft/sarif-tools

   ```
   # Install a virtual invironment, if desired:
   python3 -m venv zvenv
   source zvenv/bin/activate
   pip install pip -U
   # Install sarif-tools
   pip install sarif-tools
   # See the summary in text form:
   sarif summary semgrep1.sarif
   # Generate a cvs file
   sarif csv -o semgrep1.csv semgrep1.sarif
   # Generate an html file
   sarif html -o semgrep1.html semgrep1.sarif
   ```
