# Tagging / Labeling Strategy

Tags (Azure) and labels (GCP) are the mutable metadata layer that makes cost reporting,
ownership tracking, and governance queries possible without depending on resource naming
alone (which is immutable and shouldn't encode frequently-changing information).

## Required tags/labels

| Key | Example | Purpose |
|---|---|---|
| `environment` | `prod` | Environment-based reporting and policy |
| `owner` / `team` | `platform-engineering` | Ownership and escalation contact |
| `cost-center` | `cc-4471` | Finance chargeback |
| `managed-by` | `terraform` | Signals no manual console changes expected |

## Design principles

- Required tags are **enforced via policy-as-code** (see `architecture-domains/governance.md`), not just documented as a convention — a convention nobody enforces gets violated under deadline pressure.
- Tags are for **metadata that changes** (owning team, cost center) — encode genuinely immutable facts (resource type, primary purpose) in the resource name instead, per `best-practices/naming-conventions.md`.
- Every project/subscription gets required tags at **creation time** via the project factory pattern (see the companion `gcp-landing-zone` repository), not retrofitted later.

## Common mistakes

- Treating tagging as optional/best-effort instead of policy-enforced, leading to inconsistent coverage that undermines cost reporting.
- Using tags for information that should be in the resource name (immutable, structural facts) or vice versa.
- Allowing tag values to drift into inconsistent casing/spelling (`Prod` vs `prod` vs `PROD`) without validation.

## Further Reading

- `architecture-domains/governance.md`
- `best-practices/naming-conventions.md`, `best-practices/governance-checklist.md`
