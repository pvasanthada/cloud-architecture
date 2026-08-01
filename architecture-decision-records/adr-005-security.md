# ADR-005: Policy-as-Code Enforcement in CI, Not Manual Review Alone

**Status:** Accepted

**Date:** 2026-04-22

**Deciders:** Principal Cloud Architect, Security Lead, Platform Engineering Lead

## Context

Following ADR-003 (group-based IAM only) and ADR-001/002 (landing zone structure), we need a mechanism to actually enforce these decisions over time, as more engineers contribute Terraform changes to the landing zone. Manual PR review alone has historically missed violations — the individual-binding pattern ADR-003 exists to eliminate was itself introduced gradually through manually reviewed PRs where reviewers didn't catch every instance.

## Decision

We will enforce our IAM binding policy (group-only), required tagging/labeling standard, and public-storage-access restrictions using **Open Policy Agent (OPA) evaluated against the Terraform plan JSON in CI**, blocking any plan that violates policy before it can be applied — in addition to, not instead of, manual PR review.

## Alternatives Considered

- **Manual review only, with a documented checklist**:
  - Considered as the lower-effort option, and it's what we'd been doing.
  - Rejected because it had already demonstrably failed to catch the exact violations we're now trying to prevent — reviewer attention doesn't scale reliably with PR volume, especially under delivery deadline pressure.

- **HashiCorp Sentinel (requires Terraform Cloud/Enterprise)**:
  - Considered since it's HashiCorp's native policy engine.
  - Rejected primarily due to cost and platform lock-in — we're using self-hosted state backends (GCS/Azure Storage) rather than Terraform Cloud, and OPA/Conftest works against plan JSON regardless of backend, fitting our existing CI setup with less migration cost.

## Consequences

### Positive

- Policy violations are caught automatically, before apply, with a specific and actionable error message — not discovered later in a security audit or, worse, not discovered at all.
- New engineers get immediate feedback on policy violations in CI rather than depending entirely on a reviewer catching it.
- Policy rules are version-controlled, auditable, and testable themselves, alongside the infrastructure they govern.

### Negative

- Requires initial investment in writing and testing Rego policies, plus ongoing maintenance as new policy needs emerge.
- False positives in poorly written policy rules can block legitimate work and erode trust in the policy gate if not addressed quickly — this requires the platform team to treat policy rule quality as an ongoing responsibility.

### Neutral

- This is a pipeline-time control, not a runtime one — we still rely on Org Policy (runtime, cloud-native) as a backstop against any change made outside our Terraform CI pipeline entirely (e.g., a console change), consistent with the defense-in-depth principle in `architecture-domains/security.md`.

## Trade-offs

| Factor | OPA/Conftest in CI (chosen) | Manual Review Only (rejected) | Sentinel (rejected) |
|---|---|---|---|
| Catches violations before apply | Yes, automatically | Unreliably, depends on reviewer attention | Yes, automatically |
| Platform/backend requirement | None — works with any backend | None | Requires Terraform Cloud/Enterprise |
| Upfront investment | Moderate — write and test policies | Low | Moderate-High — licensing plus policy authoring |

## Further Reading

- Companion repository: `terraform-enterprise`, `docs/08-policy-as-code.md`
- `architecture-domains/governance.md`, `architecture-domains/security.md`
