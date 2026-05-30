# HT-320: Prepare production cohort setup and go/no-go review

**Priority:** P1
**Repo:** backend / frontend / docs / tickets
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Prepare the live partner cohort configuration and record the final pilot go/no-go decision.

## Description

HT-314 through HT-317 make the partner cohort path technically measurable. This ticket turns that into a launch checkpoint: production cohort configuration, invite semantics, consent copy version, migrations, smoke test, monitoring and final decision.

## Dependencies

- HT-315: insurer invite and onboarding
- HT-316: prevention tasks and reminders
- HT-317: pilot analytics, reporting and readiness review
- HT-318: pilot support and incident runbook
- HT-319: data deletion and consent withdrawal runbook

## Expected Files

- `hometruth DOCS/docs/product/pilot-go-no-go-review.md`
- `HomeTruth-tickets/open/HT-320-production-cohort-setup-go-no-go.md`

## Acceptance Criteria

- [ ] Production/staging target environment is confirmed.
- [ ] Partner record and cohort record are configured with target size, status, cohort key and dates.
- [ ] Invite mode is confirmed: cohort code, individual invite codes or both.
- [ ] Consent copy version is recorded.
- [ ] Required and optional consent scopes are reviewed.
- [ ] End-to-end smoke test covers invite view, auth, consent, property setup, task generation and admin cohort report.
- [ ] `npm run db:migrate:status` is recorded for the target backend environment.
- [ ] Admin pilot report is reviewed for aggregate-only output.
- [ ] Open risks and blockers are listed.
- [ ] Final `go`, `go_with_monitoring` or `no_go` decision is recorded with owner/date.

## Review / Decision Gate

This is the final launch gate. It should remain `no_go` until HT-318 and HT-319 are accepted and the target environment has been smoke-tested.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-320 from HT-317 final readiness gate.
- Verification: ticket derived from completed technical pilot path and open operational blockers.
- Notes: this is not a new product feature ticket; it is the launch control point.
