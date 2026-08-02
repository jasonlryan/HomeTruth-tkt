# HT-328: Define the B2B2C partner-programme scope

**Priority:** P1
**Repo:** docs / tickets
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-08-02

## Goal

Turn the current insurer-pilot implementation into a deliberate B2B2C product direction: a repeatable partner programme that preserves homeowner control and does not become bespoke partner delivery.

## Objective

Define the common partner-programme model, choose the initial commercial wedge, document partner and homeowner stories, distinguish shared capabilities from vertical packs, and sequence implementation work.

## Scope

- Insurers, mortgage providers and new-build companies as future B2B partner segments.
- Insurer-sponsored prevention and engagement as the first implementation wedge.
- Partner personas, homeowner boundary, common lifecycle, data/consent principles and phase gates.
- A sequenced backlog for the partner pilot kit, governance, integrations and insurer pack.

## Out Of Scope

- Building partner product functionality in this ticket.
- Committing to an external partner, commercial terms or data-sharing agreement.
- Designing a separate bespoke application for every segment.
- Default individual-data sharing or partner task/property control.

## Acceptance Criteria

- [x] A B2B2C product objective is documented.
- [x] Insurer, mortgage-provider and new-build segments are captured.
- [x] The initial insurer wedge is stated with its rationale.
- [x] Partner and homeowner roles, jobs and lifecycle stories are documented.
- [x] Shared core capabilities are separated from vertical packs.
- [x] Data, consent and access principles are explicit.
- [x] Phase gates and success measures are defined.
- [x] Follow-up implementation tickets are created and ordered.
- [ ] Product owner accepts the scope and confirms the first design-partner route.

## Dependencies

- HT-314: partner cohort and consent foundation
- HT-315: invite-led partner onboarding
- HT-317, HT-324 and HT-326: pilot reporting and repeat-use foundations
- HT-320: current live-cohort go/no-go remains independent and must not be bypassed

## Agent Delivery Protocol

Follow the HomeTruth Agent Delivery Playbook in the documentation repository:

- HT-328 is documentation/ticket work and is committed directly to main.
- HT-329 onward contain code work. Any code change uses the installed pr-review-fix-loop skill: ticketed feature branch, one draft PR, review from a clean target-branch worktree, fixes only on the feature branch, repeat until clear to merge, then one ready-for-review transition and CI check.
- Main is the current expected HomeTruth target branch, but agents must inspect repository authority and use dev if that repository's conventions require it.
- Do not create PRs solely for documentation or ticket updates.

## Implementation Log

### 2026-08-02
- Repo: docs, tickets
- Changed: created the B2B2C partner-programme scope and next-phase backlog.
- Verification: scope links existing insurer-pilot foundations to reusable partner roles, lifecycle and governed reporting requirements.
- Notes: no code is implied by this ticket; implementation begins only after the scope gate is accepted.
