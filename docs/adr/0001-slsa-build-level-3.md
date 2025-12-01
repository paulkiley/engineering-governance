# ADR 0001: Implement SLSA Build Level 3

Date: 2025-12-01

## Status

Accepted

## Context

Supply chain security is critical for software artifacts. The SLSA (Supply-chain Levels for Software Artifacts) framework provides a maturity model for build integrity. We needed to:

1. Provide verifiable provenance for build artifacts
2. Enable downstream consumers to trust our artifacts
3. Demonstrate security maturity for enterprise contexts

## Decision

Implement SLSA Build Level 3 using GitHub's native attestation framework:

- Use `actions/attest-build-provenance@v1` for signed provenance
- Create a reusable workflow (`reusable-ci-slsa-l3.yml`) for consistency
- Leverage GitHub's Sigstore integration for cryptographic signing
- Make attestations verifiable via `gh attestation verify`

## Consequences

**Positive:**
- Artifacts have cryptographically signed provenance
- Verifiable claims about build origin and process
- Achieves maximum defined SLSA level (L4 deferred in spec)
- Differentiates from repos without supply chain security

**Negative:**
- Attestations only work on public repos (GitHub free tier)
- Adds ~30s to CI pipeline for attestation step
- Requires callers to set specific permissions

**Neutral:**
- L3 is sufficient; L4 (hermetic builds) not yet defined in SLSA v1.0/v1.1

## Alternatives Considered

1. **SLSA L1 only** - Just provenance existence. Rejected: too weak for enterprise contexts.
2. **SLSA L2** - Hosted build + signed provenance. Rejected: L3 achievable with same effort.
3. **Self-hosted signing** - Use our own keys. Rejected: GitHub/Sigstore more trustworthy.
4. **Wait for L4** - Deferred indefinitely in spec. Rejected: L3 is current maximum.

## References

- [SLSA v1.0 Levels](https://slsa.dev/spec/v1.0/levels)
- [GitHub Artifact Attestations](https://docs.github.com/en/actions/security-for-github-actions/using-artifact-attestations)
- [Sigstore](https://www.sigstore.dev/)
