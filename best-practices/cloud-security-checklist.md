# Cloud Security Checklist

A condensed, practical checklist derived from `architecture-domains/security.md` and
`cloud-patterns/zero-trust.md`.

## Identity

- [ ] All IAM bindings target groups, never individual users (see `architecture-domains/identity.md`)
- [ ] MFA enforced for all human access, hardware-key-based for privileged (Tier 0) access
- [ ] No standing broad roles (Owner/Editor equivalents) outside a small, tightly controlled platform tier

## Network

- [ ] Default-deny segmentation enforced at the folder/management-group level, not just per-project
- [ ] No implicit trust granted based on network location alone ("internal" traffic still verified)
- [ ] Public IP / public access disabled by default, requiring explicit, reviewed exception

## Data

- [ ] Encryption at rest and in transit enabled by default
- [ ] Secrets referenced from a centralized secret store at runtime, never passed as plain configuration
- [ ] Public bucket/container access prevention enabled by default

## Detection

- [ ] Centralized, org-wide audit logging in place, not per-project silos
- [ ] Control-plane changes (IAM, policy) alert at the highest severity
- [ ] Alerting has a staffed, on-call response capability — not just configured, but acted on

## Common mistakes

- Configuring detection tooling without staffing a response capability to act on what it surfaces.
- Applying strict controls uniformly without regard to actual risk, driving workarounds.
- Treating this checklist as a one-time audit instead of continuous, policy-as-code-enforced practice.

## Further Reading

- `architecture-domains/security.md`, `cloud-patterns/zero-trust.md`
- `reference-architectures/secure-enterprise.md`
