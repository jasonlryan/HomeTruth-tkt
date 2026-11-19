# HT-339: Validate the first personal-agent connection and platform rollout

**Priority:** P1
**Repo:** backend / frontend / docs
**Created:** 2026-10-25
**Status:** Planned, not implemented

## Objective

Prove the first OpenAI/ChatGPT Dots connection on intended accounts before announcing availability or adding other platforms.

## Scope

Account/surface/region eligibility; private pilot; approval/publication requirements; evidence-backed homeowner task; support and commercial measures.

## Out Of Scope

Guaranteed platform approvals, multi-platform availability by inference, scheme membership by inference, and unapproved production sharing.

## Implementation Workstreams

1. Agree and record the bounded contract and unresolved external decisions.
2. Implement on a ticket-named feature branch only after its contract is accepted.
3. Complete focused and dependency-path validation, base-branch review/fixes and one PR per implementation repository.

## Acceptance Criteria

- [ ] Named pilot owner, payer, participant consent and success thresholds.
- [ ] First platform answers the agreed task with sources and unknowns.
- [ ] Revocation and second-user denial pass end to end.
- [ ] Each later platform has a separate compatibility and release decision.
- [ ] Website availability changes only after recorded deployment and approval evidence.

## Required Verification

Exact-account end-to-end task, unsupported action, denial/revocation and failure/recovery; useful-answer/return-use/cost measures; target-environment rehearsal.

## Dependencies And Decisions

HT-335 plan: `hometruth DOCS/docs/product/personal-agent-opda-delivery-plan.md`. Follow the workstream sequence and external approval gates there. No technical owner, budget or delivery date is assumed.

## HT-FLOW-005 database requirements

**Reuse.** Use the HT-337 grant and HT-338 evidence-backed response to exercise a named provider on its actual surface.

**Missing or required.** Record the tested operation, provider surface, cohort or region, validation evidence and release decision. A successful private test establishes eligibility for that cohort only.

**Decision needed.** Who owns provider eligibility, approval and withdrawal, and where should those decisions be maintained?

This records planning requirements only. Connect your agent remains on the roadmap.
