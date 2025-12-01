# Engineering Governance

Reusable CI/CD workflows, templates, and governance patterns for software projects.

## Features

- **SLSA Build Level 3** - Cryptographically signed provenance attestations
- **Reusable CI Workflows** - Python linting, security scanning, documentation
- **Project Templates** - Copier-based scaffolding with governance built-in
- **ADR Templates** - Architecture Decision Records

## SLSA Build Level 3

This repo provides a reusable workflow that achieves [SLSA Build Level 3](https://slsa.dev/spec/v1.0/levels) - the highest level defined in the current specification.

### What SLSA L3 Provides

| Level | Requirement | Status |
|-------|-------------|--------|
| L1 | Provenance exists | ✅ |
| L2 | Hosted build + signed provenance | ✅ |
| L3 | Hardened builds (runner isolation) | ✅ |
| L4 | Hermetic builds | N/A (deferred in spec) |

### Usage

```yaml
# In your repo's .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main]
  pull_request:

permissions:
  id-token: write
  contents: read
  attestations: write

jobs:
  ci:
    uses: paulkiley/engineering-governance/.github/workflows/reusable-ci-slsa-l3.yml@main
    with:
      python-version: '3.11'
      attest: true
    permissions:
      id-token: write
      contents: read
      attestations: write
```

### Verify Attestations

```bash
# Download artifact from a workflow run
gh run download <run-id> -n build-artifacts

# Verify the attestation
gh attestation verify build-artifacts.tar.gz --repo <your-repo>
```

## Standard CI (Without Attestations)

For repos that don't need SLSA attestations:

```yaml
jobs:
  ci:
    uses: paulkiley/engineering-governance/.github/workflows/reusable-ci.yml@main
    with:
      python-version: '3.11'
```

### CI Jobs Included

- **build-validate** - Manifest generation and validation
- **lint-python** - Ruff + Black
- **security-scan** - Bandit + Gitleaks
- **lint-docs** - Markdownlint + Yamllint

## Project Templates

Scaffold new projects with governance built-in:

```bash
copier copy gh:paulkiley/engineering-governance my-new-project
```

Includes:
- GitHub issue/PR templates
- CODEOWNERS
- CONTRIBUTING.md
- SECURITY.md
- ADR template

## Architecture Decision Records

See [docs/adr/](docs/adr/) for decision records. Use the template:

```bash
cp docs/adr/_template.md docs/adr/NNNN-title.md
```

## References

- [SLSA Specification v1.0](https://slsa.dev/spec/v1.0/)
- [GitHub Artifact Attestations](https://docs.github.com/en/actions/security-for-github-actions/using-artifact-attestations)
- [Copier](https://copier.readthedocs.io/)
