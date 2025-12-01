# Security Policy

## Reporting Vulnerabilities

**Do not open public issues for security vulnerabilities.**

Report vulnerabilities privately:
1. Go to the repository's **Security** tab
2. Click **Report a vulnerability**
3. Provide details and steps to reproduce

We will respond within 48 hours and work with you on a fix.

## Security Measures

This project uses:
- **SLSA Build Level 3** - Cryptographically signed provenance
- **Gitleaks** - Secret scanning in CI
- **Bandit** - Python security linting
- **Dependabot** - Dependency updates

## Verification

Verify artifact provenance:
```bash
gh attestation verify <artifact> --repo <this-repo>
```
