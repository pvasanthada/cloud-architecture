# Governance Checklist

A condensed, practical checklist derived from `architecture-domains/governance.md`. Use this
during project creation and periodic reviews.

## Project/subscription creation

- [ ] Created through the project factory / landing zone pipeline, never manually in a console
- [ ] Required tags/labels present (`environment`, `owner`, `cost-center`, `managed-by`)
- [ ] Budget configured with alert thresholds at creation time (50/80/100%)
- [ ] Correct folder/management group placement for its environment and business unit
- [ ] Required APIs/resource providers enabled explicitly, not broadly

## Ongoing governance

- [ ] Org Policy / Azure Policy exceptions tracked with a documented, linked justification
- [ ] Quarterly access review of group membership against team rosters
- [ ] Policy-as-code (OPA/Sentinel) checks passing in CI for every infrastructure change
- [ ] Budget breaches have a designated owner who actually reviews and acts on them

## Periodic architecture review

- [ ] Folder/management group hierarchy still reflects actual organizational structure (see `architecture-principles/enterprise-architecture.md`)
- [ ] Shared services capacity (NAT, logging ingestion) reviewed against current workload count
- [ ] No individual (non-group) IAM bindings present — automated check, not just manual spot-check

## Common mistakes

- Treating this checklist as a one-time setup gate instead of a recurring review practice.
- Tracking policy exceptions informally (a Slack thread) instead of in a reviewable, linked record.

## Further Reading

- `architecture-domains/governance.md`
- `best-practices/architecture-review-checklist.md`
