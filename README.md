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

1. `semgrep-01.yml` uses a `run:` step with a direct 
   `docker run` invocation.

2. `semgrep-02.yml` uses a
   ```
   container:
     image:
   ```
   format.


## Code Checkout

1. The usual/simple approach consists in scanning the code
   contained in the **same** repository that contains triggered
   workflows. We use this straightforward approach in 
   `sv-security-scans-01`, `-02`, `-03`,`-04`, `-05a`.

2. Here we use a slightly different scheme by checking
   out and scanning the code from another repo/branch. This way we
   avoid copying the same code to be scanned into every new
   repository.

3. Note that unlike Azure DevOps, in GitHub you cannot easily trigger
   the current repo's workflow by a change in another repo/branch
   (which is standard/straightforward in Azure DevOps).


## SARIF: Static Analysis Results Interchange Format

1. Even though Semgrep is capable to generate `.sarif` files
   (https://sarifweb.azurewebsites.net/), which you can 
   upload to GitHub and browse their nice representation there,
2. the action `github/codeql-action/upload-sarif@v2`
   required to upload `.sarif` files assumes that you have
   GHAS (GitHub Advanced Security license). This is a catch:
   Semgrep (no GHAS needed) generates a desired `.sarif`,
   but you cannot upload it to GitHub (requires GHAS).
3. To read `.sarif files` you may find useful Python 
   command line tools https://github.com/microsoft/sarif-tools:

   ```
   # Install a virtual environment, if desired:
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


## References

Have a look at repositories:

1. https://github.com/solita/sv-security-scans-01 (internal)
   containing samples workflow for several excellent open-source 
   security tools invocations. You do not have to have licenses.
2. https://github.com/solita/sv-security-scans-05a (public)
   containing workflow for Bandit (Python SAST) and Snyk
   (commercial but relies on a free tier). Notice that scans 
  in this repo are located on **branches**, not only **main**.
