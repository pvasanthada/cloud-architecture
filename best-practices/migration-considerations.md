# Migration Considerations

Practical considerations when migrating workloads onto a new landing zone or between
clouds, derived from `architecture-principles/cloud-adoption-framework.md`.

## Before migrating a workload

- [ ] Rationalization decision made explicitly: migrate as-is, replatform, rearchitect, or retire — not defaulted uniformly
- [ ] RTO/RPO requirements established for this specific workload (see `architecture-domains/disaster-recovery.md`)
- [ ] Data residency/compliance requirements identified before, not after, choosing a target region
- [ ] Landing zone foundation (network, IAM, governance) already exists — don't migrate onto ungoverned infrastructure

## During migration

- [ ] Non-overlapping IP address space confirmed between source and target environments
- [ ] Identity federation in place before cutover, not improvised during it
- [ ] A tested rollback plan exists in case cutover needs to be reversed

## After migration

- [ ] Old environment decommissioned on a defined timeline — lingering "just in case" parallel infrastructure is a common source of ongoing unnecessary cost
- [ ] Observability confirmed working in the new environment before fully retiring old monitoring
- [ ] Runbooks and on-call documentation updated to reflect the new environment

## Common mistakes

- Lift-and-shifting every workload uniformly instead of rationalizing case by case.
- Skipping the landing zone step under deadline pressure, then retrofitting governance later at much higher cost (see `architecture-principles/cloud-adoption-framework.md`'s real enterprise scenario).
- Never decommissioning the old environment, silently doubling infrastructure cost indefinitely.

## Further Reading

- `architecture-principles/cloud-adoption-framework.md`
- `case-studies/enterprise-modernization.md`, `case-studies/hybrid-cloud-strategy.md`
