# Cloud Architecture — An Enterprise Cloud Architecture Knowledge Base

![Architecture](https://img.shields.io/badge/Focus-Enterprise%20Architecture-4285F4)
![Azure](https://img.shields.io/badge/Azure-Reference%20Architectures-0078D4?logo=microsoftazure&logoColor=white)
![GCP](https://img.shields.io/badge/Google%20Cloud-Reference%20Architectures-4285F4?logo=googlecloud&logoColor=white)
![License](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)
![Status](https://img.shields.io/badge/Status-Living%20Document-success)
![PRs](https://img.shields.io/badge/PRs-welcome-brightgreen)

> A public knowledge base of enterprise cloud architecture thinking — design principles, reference architectures, decision records, patterns, and case studies — written the way a Principal Architect actually reasons through a design, not the way a tutorial explains a service.

## Overview

This repository is not a tutorial and not a lab guide. It's a structured record of **architecture thinking**: the trade-offs behind a hub-and-spoke topology versus a mesh, the reasoning that leads to a Landing Zone design, the conversation a Principal Architect has with a CFO about active-active versus active-passive disaster recovery. Where implementation repositories show *how* to build something, this repository shows *how to decide what to build and why*.

It spans both Azure and Google Cloud, and treats AI platform architecture and platform engineering as first-class domains alongside networking, identity, and security — because that's what an enterprise architecture practice looks like today.

## Why This Repository Exists

Most public cloud content falls into two categories: vendor documentation (accurate, but focused on *how* a service works) and tutorials (focused on getting a demo running). Neither captures the layer in between — the judgment calls: When is a shared VPC/VNet the right call versus per-team networks? When does a landing zone need a second hub? What does a real enterprise's disaster recovery conversation actually sound like, including the parts where the "textbook" answer isn't what the business chooses?

This repository exists to document that layer, in the open, the way an architecture team's internal wiki would — if that wiki were written for public consumption and put through editorial rigor.

## Learning Roadmap

If you're using this repository to build architecture judgment (for interview preparation, a certification, or genuine skill-building), read in this order:

1. **[architecture-principles/](architecture-principles)** — the reasoning frameworks underneath everything else
2. **[cloud-patterns/](cloud-patterns)** — the recurring topologies you'll reach for repeatedly
3. **[architecture-domains/](architecture-domains)** — deep dives per domain (networking, identity, security, etc.)
4. **[architecture-decision-records/](architecture-decision-records)** — see the patterns and domains applied to real decisions
5. **[reference-architectures/](reference-architectures)** — see it all composed into complete platforms
6. **[case-studies/](case-studies)** — see it applied under real organizational constraints
7. **[best-practices/](best-practices)** — the condensed checklists you'll actually use day to day

## Repository Structure

```
cloud-architecture/
├── architecture-principles/       # Foundational reasoning frameworks
├── cloud-patterns/                # Reusable architectural topologies
├── architecture-domains/          # Deep dives per architecture domain
├── architecture-decision-records/ # Realistic ADRs in industry-standard format
├── reference-architectures/       # Complete, composed platform designs
├── diagrams/                      # Draw.io architecture diagram sources
├── best-practices/                # Condensed checklists and standards
├── case-studies/                  # Realistic enterprise scenarios end-to-end
├── references/                    # Curated external reading
└── assets/                        # Supporting images
```

## Architecture Domains

| Domain | Description |
|---|---|
| [Networking](architecture-domains/networking.md) | Topology, segmentation, connectivity design |
| [Identity](architecture-domains/identity.md) | Identity federation, access models, Zero Trust foundations |
| [Governance](architecture-domains/governance.md) | Policy, guardrails, cost management at scale |
| [Security](architecture-domains/security.md) | Defense in depth, threat modeling, secure-by-design |
| [Observability](architecture-domains/observability.md) | Logging, monitoring, tracing, SRE practice |
| [Platform Engineering](architecture-domains/platform-engineering.md) | Internal developer platforms, golden paths |
| [Kubernetes](architecture-domains/kubernetes.md) | Multi-tenant cluster architecture, platform patterns |
| [Storage](architecture-domains/storage.md) | Data tiering, durability, access patterns |
| [Compute](architecture-domains/compute.md) | Workload placement, autoscaling, cost/performance trade-offs |
| [Disaster Recovery](architecture-domains/disaster-recovery.md) | RTO/RPO-driven resilience design |

## Reference Architectures

| Architecture | Description |
|---|---|
| [Enterprise Azure](reference-architectures/azure-enterprise.md) | Complete Azure enterprise foundation |
| [Enterprise GCP](reference-architectures/gcp-enterprise.md) | Complete Google Cloud enterprise foundation |
| [Hybrid Cloud](reference-architectures/hybrid-cloud.md) | On-prem + multi-cloud composed architecture |
| [AI Platform](reference-architectures/ai-platform.md) | Enterprise AI/ML platform architecture |
| [Kubernetes Platform](reference-architectures/kubernetes-platform.md) | Multi-tenant Kubernetes platform |
| [Secure Enterprise](reference-architectures/secure-enterprise.md) | Zero Trust, defense-in-depth composed architecture |

## Architecture Decision Records

This repository practices what it documents: every non-trivial design choice is captured as an ADR. See [`architecture-decision-records/`](architecture-decision-records) for realistic, industry-standard-format examples covering landing zone topology, network design, identity, Kubernetes, and security decisions — and [`adr-template.md`](architecture-decision-records/adr-template.md) for the template itself.

## Best Practices

Condensed, checklist-form references for day-to-day architecture work: [naming conventions](best-practices/naming-conventions.md), [tagging strategy](best-practices/tagging-strategy.md), [governance checklist](best-practices/governance-checklist.md), [architecture review checklist](best-practices/architecture-review-checklist.md), [cloud security checklist](best-practices/cloud-security-checklist.md), and [migration considerations](best-practices/migration-considerations.md).

## Design Principles

Every document in this repository is written against the same underlying principles, laid out in [`architecture-principles/design-principles.md`](architecture-principles/design-principles.md): optimize for the organization's actual constraints, not textbook ideals; make trade-offs explicit; prefer boring, well-understood technology at the core; and design for the operability the team will actually have, not the operability a larger team could provide.

## Architecture Review Process

Enterprise architecture decisions in this repository's case studies and ADRs follow a consistent review discipline, documented in [`best-practices/architecture-review-checklist.md`](best-practices/architecture-review-checklist.md): a proposal states the business problem before the technical solution, alternatives are documented even when rejected, and every review explicitly covers security, cost, and operability — not just "does it work."

## Technology Coverage

This repository is intentionally **multi-cloud in perspective, not multi-cloud in every design** — most reference architectures are single-cloud by design (see [`cloud-patterns/hybrid-cloud.md`](cloud-patterns/hybrid-cloud.md) for why multi-cloud-by-default is usually the wrong call). Coverage spans Azure and Google Cloud, Kubernetes (AKS, GKE, and CNCF-ecosystem patterns generally), and hybrid/on-prem connectivity.

## AI Architecture

AI platform architecture is treated as a first-class domain, not an afterthought bolted onto existing infrastructure. See [`reference-architectures/ai-platform.md`](reference-architectures/ai-platform.md) for a complete enterprise AI/ML platform design, and [`case-studies/ai-cloud-adoption.md`](case-studies/ai-cloud-adoption.md) for how a real organization's AI adoption interacts with existing governance and security posture.

## Platform Engineering

Platform engineering — building the internal platform that application teams consume — is covered both as a principle ([`architecture-principles/platform-engineering.md`](architecture-principles/platform-engineering.md)) and as a domain deep-dive ([`architecture-domains/platform-engineering.md`](architecture-domains/platform-engineering.md)), reflecting how central this discipline has become to enterprise cloud strategy.

## Documentation Index

<details>
<summary>Full file index (click to expand)</summary>

**architecture-principles/**: design-principles, architecture-decision-records, enterprise-architecture, cloud-adoption-framework, platform-engineering

**cloud-patterns/**: hub-spoke, mesh-network, landing-zone, shared-services, multi-region, active-active, active-passive, zero-trust, hybrid-cloud

**architecture-domains/**: networking, identity, governance, security, observability, platform-engineering, kubernetes, storage, compute, disaster-recovery

**architecture-decision-records/**: adr-001-landing-zone, adr-002-network-design, adr-003-identity, adr-004-kubernetes, adr-005-security, adr-template

**reference-architectures/**: azure-enterprise, gcp-enterprise, hybrid-cloud, ai-platform, kubernetes-platform, secure-enterprise

**best-practices/**: naming-conventions, tagging-strategy, governance-checklist, architecture-review-checklist, cloud-security-checklist, migration-considerations

**case-studies/**: enterprise-modernization, landing-zone-implementation, hybrid-cloud-strategy, kubernetes-adoption, ai-cloud-adoption

**references/**: books, microsoft, google, cncf, architecture-frameworks

</details>

## Roadmap

- [ ] Add AWS-perspective reference architectures for full three-cloud coverage
- [ ] Add a FinOps-focused domain deep-dive
- [ ] Add a data platform / data mesh reference architecture
- [ ] Add more case studies (public sector, SaaS scale-up)
- [ ] Add architecture katas / practice scenarios for interview preparation

## Contributing

Contributions are welcome — see [`CONTRIBUTING.md`](CONTRIBUTING.md). This repository holds every document to the same structural standard (Overview through Further Reading); new documents should follow it.

## License

Content is licensed under [CC BY 4.0](LICENSE) — reuse and adapt freely with attribution.
