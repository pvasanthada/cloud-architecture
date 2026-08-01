# Architecture Review Checklist

The review discipline this repository's own ADRs and reference architectures follow — use
this when reviewing any significant architecture proposal.

## Before the review

- [ ] The proposal states the business problem before the technical solution
- [ ] Alternatives were genuinely considered and are documented, even the rejected ones (see `architecture-decision-records/adr-template.md`)
- [ ] RTO/RPO or equivalent explicit requirements are stated for anything resilience-related (see `architecture-domains/disaster-recovery.md`)

## During the review

- [ ] Security: identity, network segmentation, and data protection are addressed explicitly, not assumed
- [ ] Cost: order-of-magnitude cost estimate provided, including ongoing operational cost, not just build cost
- [ ] Operability: the team that will operate this has the skills and capacity to do so (see `architecture-principles/design-principles.md`)
- [ ] Trade-offs are stated honestly — a proposal with no listed disadvantages hasn't been reasoned through fully

## After the review

- [ ] Decision (and rejected alternatives) captured as an ADR
- [ ] Follow-up items have owners and dates, not just a general intention

## Common mistakes

- Reviewing only the happy path, without asking what happens under failure conditions.
- Treating security and cost as follow-up concerns to address after the "real" design review.
- Approving a proposal without documenting why alternatives were rejected, losing that reasoning for future reference.

## Further Reading

- `architecture-principles/architecture-decision-records.md`
- `architecture-decision-records/adr-template.md`
