# ADR-001: Environment-First Folder Hierarchy for the Landing Zone

**Status:** Accepted

**Date:** 2026-02-14

**Deciders:** Principal Cloud Architect, Platform Engineering Lead, Security Lead

## Context

We are designing the top-level folder hierarchy for our GCP landing zone. Our organization has three business units (Payments, Storefront, Data Platform), each needing production and non-production environments, plus a small number of platform-owned shared services. We need a folder structure that Org Policy and IAM can inherit from cleanly, and that scales as we add business units through organic growth and acquisition.

Two structural options are on the table: environment-first (Production/Non-Production/Sandbox at the top level, business units nested inside) and business-unit-first (each business unit at the top level, environments nested inside).

## Decision

We will use an **environment-first** folder hierarchy: `Bootstrap`, `Common`, `Production`, `Non-Production`, and `Sandbox` at the top level, with business-unit folders nested under `Production` and `Non-Production`.

## Alternatives Considered

- **Business-unit-first hierarchy**: each business unit (Payments, Storefront, Data Platform) as a top-level folder, with Production/Non-Production nested inside each.
  - Considered because it simplifies cost allocation and gives each business unit full autonomy over their own subtree.
  - Rejected because our primary risk driver is blast radius of a production incident, not cost allocation (which we can solve with labels and billing export instead) — and business-unit-first would require duplicating Org Policy differences between environments across every business unit folder instead of setting them once.

- **Flat structure, no folders, projects directly under the organization**: 
  - Considered briefly for simplicity.
  - Rejected immediately — this provides no IAM/policy inheritance boundary at all and doesn't scale past a handful of projects.

## Consequences

### Positive

- A single Production Org Policy set (stricter constraints) and a single Non-Production Org Policy set (relaxed) apply automatically to every business unit's projects in that environment — no per-business-unit policy duplication.
- New business units (including ones we acquire) slot cleanly into the existing Production/Non-Production structure without redesigning policy.

### Negative

- Cost allocation by business unit requires consistent labeling and billing export queries rather than being implicit in folder structure — this is solvable but is genuinely extra work compared to business-unit-first.
- Business units have less structural autonomy over their own subtree than they would under business-unit-first.

### Neutral

- This decision is specific to our current risk model (production incident blast radius as the primary concern); if cost allocation becomes the dominant organizational pain point instead, this decision should be revisited.

## Trade-offs

| Factor | Environment-First (chosen) | Business-Unit-First (rejected) |
|---|---|---|
| Org Policy duplication | None — set once per environment | Required per business unit per environment |
| Cost allocation | Requires labels + billing export | Implicit in folder structure |
| Business unit autonomy | Lower | Higher |
| Acquisition integration | New BU folder added under existing environment folders | New BU folder plus its own environment sub-structure |

## Further Reading

- Companion repository: `gcp-landing-zone`, `docs/03-folder-hierarchy.md`
- `cloud-patterns/landing-zone.md`
