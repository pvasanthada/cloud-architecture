# Contributing to cloud-architecture

Thanks for considering a contribution. This repository is held to an editorial standard
closer to a publication than a code repository: **every document must be original,
well-reasoned, and structurally consistent with the rest of the repository.**

## Ways to contribute

- Propose a new cloud pattern, domain deep-dive, or reference architecture
- Add a realistic case study from a different industry vertical
- Add or refine an ADR demonstrating a specific class of trade-off
- Improve a diagram (`.drawio` sources preferred over static images)
- Fix inaccuracies, broken cross-references, or outdated service names

## Document structure standard

Every document under `architecture-principles/`, `cloud-patterns/`, `architecture-domains/`,
and `reference-architectures/` must contain, in order:

1. Overview
2. Business Problem
3. Architecture
4. Design Decisions
5. Decision Trade-offs
6. Advantages
7. Disadvantages
8. Security Considerations
9. Operational Considerations
10. Cost Considerations
11. Scalability
12. Availability
13. Real Enterprise Scenario
14. Common Mistakes
15. Interview Questions
16. Summary
17. Further Reading

If you add a new document under these directories, follow this structure exactly. If you
edit an existing one, don't remove sections.

## Writing style

Write like a Principal Architect explaining a decision to a peer review board — not like a
tutorial, not like vendor documentation, and not like AI-generated meeting notes. Every
design decision needs a stated "why," not just a "what." Trade-offs must be genuine —
if a pattern only has upsides in your writeup, you haven't looked hard enough for the
downsides.

## Diagrams

New architecture content should include both a Mermaid diagram inline in the Markdown
(renders natively on GitHub) and, where the architecture is a headline reference
architecture or pattern, a corresponding Draw.io source under `diagrams/`.

## Originality

Do not copy content from Microsoft Learn, AWS documentation, Google Cloud documentation, or
any vendor blog — even paraphrased close enough to be recognizable. This repository's value
is original architectural reasoning; content that reads like a rewritten vendor doc will be
rejected in review.

## Pull request process

1. Fork the repository and create a feature branch.
2. Write or edit content following the structure and style standards above.
3. Open a PR describing what architectural judgment the new/changed content demonstrates.
4. A maintainer will review for structural consistency, originality, and reasoning quality —
   not just accuracy.

## Code of conduct

Be respectful, be precise, and back architectural opinions with reasoning. Disagreement is
welcome; hand-waving is not.
