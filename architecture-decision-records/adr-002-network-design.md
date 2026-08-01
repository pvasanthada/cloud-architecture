# ADR-002: Shared VPC Over Per-Team VPCs for Production Networking

**Status:** Accepted

**Date:** 2026-02-21

**Deciders:** Principal Cloud Architect, Network Engineering Lead

## Context

Our Production folder will host workloads from three business units, each needing VPC networking, NAT, DNS, and firewall policy. We need to decide whether each business unit gets its own VPC (connected via peering if cross-team communication is needed) or whether all Production workloads share a single Shared VPC host project's network.

## Decision

We will use a **single Shared VPC per environment** (one for Production, one for Non-Production), with each business unit's projects attached as service projects, rather than per-team VPCs.

## Alternatives Considered

- **Per-team VPCs with VPC Peering for cross-team communication**:
  - Considered because it gives each team full autonomy over their own network configuration.
  - Rejected because VPC Peering is non-transitive — as the number of teams needing to communicate grows, peering relationships grow quadratically and become unmanageable. It also multiplies NAT gateway, Cloud Router, and DNS configuration across every team's VPC, each independently maintained.

- **Fully flat, single VPC with no host/service project separation**:
  - Considered as a simpler alternative.
  - Rejected because GCP's Shared VPC model gives us subnet-level IAM control (`roles/compute.networkUser` scoped per subnet) that a flat model doesn't provide as cleanly, and separating host (network-owning) from service (workload-owning) projects keeps network configuration changes auditable and centrally reviewed.

## Consequences

### Positive

- Single NAT/Cloud Router/DNS configuration per environment instead of duplicated per-team infrastructure.
- Cross-business-unit communication (increasingly common as Data Platform consumes events from both Payments and Storefront) works via internal IPs without any peering setup.
- Centralized hierarchical firewall policy at the folder level enforces a consistent security baseline regardless of individual team configuration.

### Negative

- The host project's IAM (`roles/compute.xpnAdmin`) is highly sensitive — misconfiguration here affects every attached service project. This requires the host project to be tightly access-controlled, understood as a Tier-0 resource.
- Business units no longer have full autonomy over their own network configuration; subnet requests go through the platform team.

### Neutral

- Isolation between business units within the Shared VPC is now enforced via IAM and hierarchical firewall policy (identity/tag-based) rather than network topology — a deliberate shift from "same VPC implies trust" to Zero Trust-style verification, consistent with ADR-005.

## Trade-offs

| Factor | Shared VPC (chosen) | Per-Team VPCs + Peering (rejected) |
|---|---|---|
| NAT/DNS/Router configuration | Once per environment | Once per team |
| Cross-team communication | Native, no extra setup | Requires peering, doesn't scale past a handful of teams |
| Team network autonomy | Lower | Higher |
| Host project IAM sensitivity | High — single point of network control | N/A — no single host project |

## Further Reading

- Companion repository: `gcp-landing-zone`, `docs/05-shared-vpc.md`
- `cloud-patterns/hub-spoke.md`
- `architecture-decision-records/adr-005-security.md`
