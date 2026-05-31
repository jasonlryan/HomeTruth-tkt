# HT-318: Define pilot support and incident runbook

**Priority:** P1
**Repo:** docs / tickets
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-31

## Goal

Make support ownership, escalation and incident handling explicit before any 500-user partner cohort is launched.

## Description

HT-317 proved the technical pilot reporting path but left operational launch blockers. This ticket closes the support and incident-response blockers so HomeTruth can handle failed onboarding, confused users, data concerns and technical incidents during the pilot.

## Dependencies

- HT-317: pilot analytics, reporting and readiness review

## Expected Files

- `hometruth DOCS/docs/product/pilot-support-incident-runbook.md`
- `HomeTruth-tickets/open/HT-318-pilot-support-incident-runbook.md`

## Acceptance Criteria

- [ ] Named pilot support owner is recorded.
- [ ] Named technical escalation contact is recorded.
- [ ] Support hours and expected first-response time are recorded.
- [x] Issue categories are defined: invite failure, login/signup, consent question, property setup, document/task issue, data deletion/withdrawal, incident.
- [x] Severity levels and escalation rules are defined.
- [x] User-facing holding responses are drafted for common pilot issues.
- [x] Incident communication path is documented.
- [x] Admin dashboard/reporting route for monitoring the pilot is referenced.
- [ ] Runbook is reviewed and accepted before pilot launch.

## Review / Decision Gate

This cannot be completed without human ownership decisions. Required inputs: support owner, technical escalation contact, incident owner and approved response expectations.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-318 from HT-317 launch blockers.
- Verification: ticket derived from completed HT-317 readiness review.
- Notes: no code required unless the support process reveals missing admin tooling.

### 2026-05-31
- Repo: docs, tickets
- Changed:
  - `hometruth DOCS/docs/product/pilot-support-incident-runbook.md`
  - `HomeTruth-tickets/open/HT-318-pilot-support-incident-runbook.md`
- Verification: drafted issue categories, severity levels, escalation rules, holding responses, incident path and admin monitoring references.
- Notes: still blocked on named support owner, technical escalation contact, incident owner, support route, support hours and first-response target.
