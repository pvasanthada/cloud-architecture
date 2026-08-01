# Recommended Books

A curated list of books that shaped the thinking in this repository. Descriptions are
original summaries, not reproduced jacket copy or reviews.

## Architecture & Systems Thinking

- **"Fundamentals of Software Architecture" — Mark Richards & Neal Ford.** A grounded treatment of architecture trade-off analysis that avoids prescribing a single "correct" architecture style, consistent with this repository's own trade-offs-first approach.
- **"Building Evolutionary Architectures" — Neal Ford, Rebecca Parsons, Patrick Kua.** Frames architecture as something that must accommodate change over time, not a static blueprint — relevant to why this repository treats ADRs (`architecture-principles/architecture-decision-records.md`) as living, superseded-not-edited records.
- **"Team Topologies" — Matthew Skelton & Manuel Pais.** The clearest treatment of Conway's Law's practical implications for platform and infrastructure team design, directly informing `architecture-principles/enterprise-architecture.md`.

## Site Reliability & Operations

- **"Site Reliability Engineering" and "The Site Reliability Workbook" — Google.** Foundational for the SLO-driven alerting philosophy in `architecture-domains/observability.md`.
- **"Accelerate" — Nicole Forsgren, Jez Humble, Gene Kim.** Empirical research connecting delivery practices to organizational performance, underpinning this repository's platform engineering emphasis on measured adoption, not just built capability.

## Security

- **"Zero Trust Networks" — Evan Gilman & Doug Barth.** The clearest technical grounding for `cloud-patterns/zero-trust.md`'s architectural stance.
- **"Threat Modeling: Designing for Security" — Adam Shostack.** Practical grounding for the defense-in-depth reasoning in `architecture-domains/security.md`.

## Platform Engineering

- **"Team Topologies"** (see above) and **"Platform Engineering on Kubernetes" — Mauricio Salatino** are the two most directly relevant texts behind `architecture-principles/platform-engineering.md` and `architecture-domains/kubernetes.md`.

## Further Reading

- `references/architecture-frameworks.md` for framework-specific (non-book) references
