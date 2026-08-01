# Architecture Frameworks

An overview of established enterprise architecture frameworks, referenced conceptually in
`architecture-principles/enterprise-architecture.md` and `architecture-principles/cloud-adoption-framework.md`.
This repository does not adopt any single framework wholesale — it borrows reasoning
patterns from several, adapted to a cloud-native context.

## TOGAF (The Open Group Architecture Framework)

A comprehensive enterprise architecture methodology covering business, data, application,
and technology architecture layers. This repository's separation of "enterprise
architecture" (organizational alignment, `architecture-principles/enterprise-architecture.md`)
from "solution architecture" (individual reference architectures) echoes TOGAF's layered
thinking, without adopting its full ADM (Architecture Development Method) process ceremony.

## Well-Architected Frameworks (Cloud-Provider-Specific)

Both Azure and Google Cloud (and AWS) publish their own Well-Architected Frameworks,
organized around similar pillars (reliability, security, cost optimization, operational
excellence, performance). This repository's `architecture-domains/` structure is
independently organized but covers substantially the same ground, applied across both
Azure and GCP rather than being provider-specific.

## Cloud Adoption Frameworks

Microsoft, Google, and AWS each publish a Cloud Adoption Framework describing staged
adoption (strategy, plan, ready, adopt, govern, manage or similar). This repository's
`architecture-principles/cloud-adoption-framework.md` describes the same staged reasoning
pattern in its own words, reflecting genuine convergent thinking across the industry on
this sequencing rather than being copied from any single vendor's specific framework.

## Zachman Framework

An older, foundational enterprise architecture classification framework (organized around
"what/how/where/who/when/why" questions across different stakeholder perspectives). Less
directly referenced in this repository's content, but a useful historical grounding for why
enterprise architecture as a discipline separates "what's being built" from "why it's being
built that way for this specific organization."

## How this repository differs from following any single framework

This repository is deliberately framework-agnostic in citation but framework-informed in
reasoning — it borrows the staged-adoption thinking common across cloud provider frameworks,
the trade-off-analysis discipline from TOGAF-style methodologies, and the pillar-based domain
organization common to Well-Architected Frameworks, without committing to any single
framework's full prescribed process, consistent with `architecture-principles/design-principles.md`'s
preference for reasoning frameworks over rigid, one-size-fits-all methodology.

## Further Reading

- `architecture-principles/enterprise-architecture.md`, `architecture-principles/cloud-adoption-framework.md`
- `references/microsoft.md`, `references/google.md`
