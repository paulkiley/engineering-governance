# Engineering Governance

Agnostic GitOps policies, reusable CI workflows, templates, and ADRs usable across projects.

## Reusable CI
Use from a project repo:
```
jobs:
  call-governance-ci:
    uses: paulkiley/engineering-governance/.github/workflows/reusable-ci.yml@v1.0.0
    with:
      python-version: '3.11'
```
