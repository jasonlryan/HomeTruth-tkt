# HT-320: Prepare production cohort setup and go/no-go review

**Priority:** P1
**Repo:** backend / frontend / docs / tickets
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-08-02

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
- HT-324: pilot reporting coverage and privacy validation

## Expected Files

- `hometruth DOCS/docs/product/pilot-go-no-go-review.md`
- `HomeTruth-tickets/open/HT-320-production-cohort-setup-go-no-go.md`

## Acceptance Criteria

- [ ] Production/staging target environment is confirmed.
- [ ] Partner record and cohort record are configured with target size, status, cohort key and dates.
- [ ] Invite mode is confirmed: cohort code, individual invite codes or both.
- [ ] Consent copy version is recorded.
- [ ] Required and optional consent scopes are reviewed.
- [ ] End-to-end smoke test covers invite view, auth, consent, property setup, document upload/link, task generation, property-aware chat and admin cohort report.
- [ ] `npm run db:migrate:status` is recorded for the target backend environment.
- [ ] Admin pilot report is reviewed for aggregate-only output.
- [x] Open risks and blockers are listed.
- [ ] Final `go`, `go_with_monitoring` or `no_go` decision is recorded with owner/date.

## Review / Decision Gate

This is the final launch gate. It should remain `no_go` until HT-318 and HT-319 are accepted and the target environment has been smoke-tested.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-320 from HT-317 final readiness gate.
- Verification: ticket derived from completed technical pilot path and open operational blockers.
- Notes: this is not a new product feature ticket; it is the launch control point.

### 2026-05-31
- Repo: docs, tickets
- Changed:
  - `hometruth DOCS/docs/product/pilot-go-no-go-review.md`
  - `HomeTruth-tickets/open/HT-320-production-cohort-setup-go-no-go.md`
- Verification: drafted go/no-go review with current `no_go` recommendation, smoke-test checklist, technical readiness checklist, operational readiness checklist and open risks.
- Notes: still blocked on target environment, partner/cohort production configuration, consent copy version, full smoke test, support ownership and privacy/deletion runbook acceptance.

### 2026-05-31
- Repo: frontend, docs, tickets
- Changed:
  - `hometruth DOCS/docs/product/pilot-go-no-go-review.md`
  - `HomeTruth-tickets/open/HT-320-production-cohort-setup-go-no-go.md`
  - HT-323 frontend property-aware chat handoff implemented in `HT_Frontend-staging`
- Verification: `npm run build` passes in `HT_Frontend-staging`.
- Notes: launch decision remains `no_go`; frontend handoff now needs target-environment smoke testing alongside the existing support, privacy/legal, target environment and consent-copy blockers.

### 2026-08-02
- Repo: backend, docs, tickets
- Changed: HT-324 technical reporting coverage now records aggregate activation, setup, document, task, chat and feedback metrics; repeat use is explicitly deferred to HT-326.
- Verification: disposable five-member local MySQL cohort smoke passed; aggregate response contract excluded individual identifiers and sensitive content.
- Notes: decision remains `no_go`. This does not replace product/pilot interpretation or privacy/compliance approval, and it is not target-environment evidence.

### 2026-08-02
- Repo: backend, frontend, docs, tickets
- Changed: HT-326 adds the repeat-use metric to the aggregate cohort report, with authenticated daily activity and no contextual metadata.
- Verification: at the time of this entry, representative local MySQL smoke passed and both HT-326 code PRs awaited review.
- Notes: superseded by the following merge entry; target-environment smoke alongside the existing operational and privacy blockers remains required.

### 2026-08-02
- Repo: backend, frontend, docs, tickets
- Changed: HT-326 backend and frontend PRs merged; backend `main` is at `0b5a164` and frontend `main` is at `2c0ccab`.
- Verification: merged mains were pulled locally; local migration and representative repeat-use smoke had already passed.
- Notes: the remaining HT-320 flight path is target-environment migration and full rehearsal, HT-327 mailbox validation, legal/privacy approval, partner configuration and final go/no-go evidence. Decision remains `no_go`.

### 2026-08-02
- Repo: docs, tickets
- Changed: Jason Ryan is recorded as interim pilot owner and go/no-go decision owner.
- Verification: owner assignment supplied directly by the pilot owner.
- Notes: decision remains `no_go` pending the target-environment rehearsal, operational/legal gates and partner configuration.

### 2026-05-31
- Repo: tickets
- Changed: added HT-324 as the follow-up for admin report metric coverage and partner-facing aggregate privacy review.
- Verification: HT-322 has metric thresholds and event mapping, but target report-field coverage and privacy approval are not yet complete.
- Notes: launch decision remains `no_go` until HT-324 is accepted or equivalent reporting/privacy sign-off is recorded.
