# HT-324: Validate pilot reporting coverage and privacy

**Priority:** P1
**Repo:** backend / docs / tickets
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-31
**Updated:** 2026-08-02

## Goal

Prove the admin cohort report can answer the 500-user pilot success metrics and that the partner-facing aggregate pack cannot leak individual user, property, document, fact, task or chat content.

## Description

HT-322 defines activation, setup, document, task, chat, repeat-use and feedback success thresholds for the pilot. The current launch plan also drafts a partner-facing aggregate reporting pack, but coverage and privacy review still need to be validated before launch.

This ticket closes that reporting gap by mapping each metric to an admin report field or event source, identifying any missing backend/reporting work, and recording product/privacy approval for the aggregate-only pack.

## Dependencies

- HT-317: pilot analytics, reporting and readiness review
- HT-322: 500-user cohort launch gap closure plan

## Expected Files

- `hometruth DOCS/docs/product/500-user-cohort-launch-plan.md`
- `hometruth DOCS/docs/product/pilot-go-no-go-review.md`
- backend reporting files if coverage gaps require code changes
- `HomeTruth-tickets/open/HT-324-validate-pilot-reporting-coverage-and-privacy.md`

## Acceptance Criteria

- [x] Each HT-322 success metric is mapped to an admin report field or source event, or explicitly marked `not_instrumented`.
- [x] Missing metrics are listed with required backend/reporting changes.
- [x] `/api/admin/pilot/cohort-report` is smoke-tested against representative pilot data.
- [ ] Partner-facing report pack is reviewed for aggregate-only output by the product/pilot owner.
- [x] Technical response-contract review confirms names, emails, addresses, document names, raw facts, task descriptions, individual chat content and individual rows are excluded.
- [ ] Product/pilot owner accepts the success metric interpretation.
- [ ] Privacy/compliance owner accepts the aggregate reporting boundary.
- [x] HT-322 and HT-320 are updated with the current technical reporting/privacy status.

## Review / Decision Gate

This ticket is complete only when the reporting pack is both analytically useful and privacy-safe. If the admin report cannot answer a metric, create or implement a concrete reporting follow-up before marking this complete.

## Implementation Log

### 2026-05-31
- Repo: tickets
- Changed: created follow-up ticket from HT-322 measurement and aggregate-reporting gap.
- Verification: HT-322 has success thresholds and event mapping, but report-field coverage and privacy review remain open.
- Notes: this is a launch blocker for partner-facing reporting, not for the core frontend property-aware chat handoff.

### 2026-08-02
- Repo: backend, docs, tickets
- Changed:
  - added distinct cohort-member metrics and aligned drop-off calculations to `/api/admin/pilot/cohort-report`
  - recorded consent-bound `property_chat_question` events without chat content
  - added `metricCoverage`, marking repeat use as `not_instrumented`
  - created HT-326 for authenticated repeat-use instrumentation
- Verification:
  - `node scripts/verifyPilotReportingCoverage.js` passes with the backend dependency path
  - representative five-member MySQL smoke passed and deleted all fixture users, partners, cohorts, members and events
  - response contract verified no user/member/property IDs, document names, raw facts, feedback text or chat content
- Notes: product/pilot owner interpretation and privacy/compliance approval remain required before external partner sharing.
