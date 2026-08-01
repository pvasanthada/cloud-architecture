# ADR-003: Group-Based IAM Bindings Only, No Individual User Bindings

**Status:** Accepted

**Date:** 2026-03-03

**Deciders:** Principal Cloud Architect, Security Lead, IAM Platform Owner

## Context

As we build out IAM for the landing zone, we need to decide our binding model: whether individual engineers can be granted IAM roles directly, or whether every binding must target a group (synced from our Cloud Identity/Workspace directory), with individual access managed entirely through group membership.

Our current (pre-landing-zone) environment has a mix of both, and a recent access review took three engineer-weeks to complete because reviewers had to individually evaluate hundreds of direct user bindings scattered across dozens of projects.

## Decision

We will require **group-based IAM bindings exclusively** for the new landing zone. No `google_project_iam_member` or equivalent binding may target an individual user account; every binding targets a Google Group. This will be enforced via a policy-as-code check in our Terraform CI pipeline (see ADR-005).

## Alternatives Considered

- **Allow individual bindings for "quick" or "temporary" access**:
  - Considered because it's genuinely faster for a one-off, time-boxed need.
  - Rejected because "temporary" individual access has, in our own historical experience, reliably become permanent — the three-week access review largely consisted of untangling exactly this kind of forgotten temporary grant. If time-boxed access is genuinely needed, IAM Conditions with an expiry are the correct mechanism, not an individual binding.

- **Individual bindings allowed only at the project level, groups required at folder/org level**:
  - Considered as a middle ground.
  - Rejected because it doesn't solve the core problem — most of our historical access review pain came specifically from project-level individual bindings, which this alternative would have left unchanged.

## Consequences

### Positive

- Offboarding becomes a single action (remove from group) instead of a project-by-project audit.
- Access reviews now mean reviewing group membership against team rosters — a task that took three weeks under the old model is now expected to take under a day per quarter.
- New engineers get correct access automatically upon group membership, rather than waiting for individual grants.

### Negative

- Requires disciplined group hygiene in our identity provider — a poorly maintained group taxonomy (too broad, or too fragmented) can recreate audit difficulty in a different form.
- Genuinely one-off access needs now require either a new, narrowly scoped group or an IAM Condition with an expiry — both have more setup overhead than a quick individual binding would.

### Neutral

- This decision requires a policy-as-code enforcement mechanism (ADR-005) to hold over time — without automated enforcement, the discipline tends to erode under delivery pressure.

## Trade-offs

| Factor | Group-Based Only (chosen) | Mixed Individual + Group (rejected) |
|---|---|---|
| Access review time (current scale) | ~1 day/quarter (projected) | ~3 engineer-weeks (observed) |
| Offboarding reliability | Atomic, single action | Requires manual audit across every project |
| One-off access setup overhead | Higher (new group or IAM Condition) | Lower (single binding) |
| Requires policy-as-code enforcement | Yes | No |

## Further Reading

- Companion repository: `gcp-landing-zone`, `docs/07-iam-security.md`
- `architecture-domains/identity.md`
- `architecture-decision-records/adr-005-security.md`
