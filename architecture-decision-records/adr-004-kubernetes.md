# ADR-004: Namespace-Based Multi-Tenancy for General Workloads, Dedicated Clusters for PCI-DSS Scope

**Status:** Accepted

**Date:** 2026-04-10

**Deciders:** Principal Cloud Architect, Platform Engineering Lead, Compliance Officer

## Context

We're designing our GKE platform to host workloads from Storefront, Data Platform, and Payments teams. Payments' workloads fall under PCI-DSS scope. We need to decide whether all teams share a common cluster fleet (namespace-isolated) or whether some or all teams get dedicated clusters.

## Decision

We will use **namespace-based multi-tenancy within a shared cluster fleet for Storefront and Data Platform workloads**, and a **dedicated, PCI-DSS-scoped cluster for Payments** workloads that fall under card-data-handling compliance scope.

## Alternatives Considered

- **Fully shared clusters for all teams, including Payments**:
  - Considered for operational simplicity and cost efficiency.
  - Rejected after consulting with our QSA (Qualified Security Assessor) — PCI-DSS node-level isolation evidence is materially harder to produce convincingly for namespace-isolated shared infrastructure than for a dedicated cluster, and the audit risk/cost outweighed the operational savings for this specific, regulated workload.

- **Fully dedicated clusters for every team**:
  - Considered for maximum isolation and simplicity of reasoning.
  - Rejected as unjustified overhead for Storefront and Data Platform, neither of which has a compliance driver requiring cluster-level isolation — the operational cost (separate control planes, separate upgrade cadences) wasn't justified by their actual risk profile.

## Consequences

### Positive

- Storefront and Data Platform get good resource utilization and lower operational overhead from shared-cluster multi-tenancy.
- Payments gets a clean, auditable isolation boundary that satisfies our QSA's node-level isolation requirement without ambiguity.
- The decision is workload-driven, not uniform, avoiding both under- and over-investment in isolation.

### Negative

- The platform team now operates two distinct cluster models (shared fleet plus a dedicated compliance-scoped cluster), which is genuinely more operational surface area than a single uniform model.
- If additional business units develop their own compliance-driven isolation requirements in the future, we may need further cluster segmentation — this decision doesn't fully future-proof against that.

### Neutral

- This decision should be revisited if Payments' workload characteristics change significantly (e.g., if card data handling scope narrows to a smaller subset of services that could be isolated at a finer grain than a whole dedicated cluster).

## Trade-offs

| Factor | Namespace Isolation (Storefront, Data Platform) | Dedicated Cluster (Payments) |
|---|---|---|
| Compliance posture for PCI-DSS | Weaker — harder to evidence node-level isolation | Strong — clean, auditable boundary |
| Operational overhead | Lower — shared control plane, shared upgrades | Higher — separate control plane and upgrade cadence |
| Resource utilization | Better bin-packing across tenants | Dedicated capacity, less shared utilization |

## Further Reading

- `architecture-domains/kubernetes.md`
- `reference-architectures/kubernetes-platform.md`
- `case-studies/kubernetes-adoption.md`
