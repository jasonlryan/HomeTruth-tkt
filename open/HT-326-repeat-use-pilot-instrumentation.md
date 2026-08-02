# HT-326: Instrument repeat use for the pilot cohort

**Priority:** P1
**Repo:** frontend / backend
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-08-02
**Updated:** 2026-08-02

## Goal

Measure whether activated cohort members return on a later day, without collecting individual browsing history or weakening the aggregate reporting boundary.

## Objective

Add an authenticated, consent-bound daily pilot activity event and extend the cohort report with a repeat-use participant count and rate. The metric must reflect activity on at least two distinct UTC days, not multiple actions in a single visit.

## Scope

### In Scope

- Add a protected backend endpoint or authenticated event path for daily pilot activity.
- Emit the event once per authenticated cohort member per UTC day from the signed-in frontend experience.
- Preserve the public invite-view event path for pre-auth invite validation.
- De-duplicate same-member, same-cohort, same-day events without storing page paths, user-entered content or property details.
- Report aggregate repeat-use participants and repeat-use rate from distinct activity dates.
- Add automated and representative-data smoke coverage.

### Out Of Scope

- Session replay, clickstream analytics or individual reporting.
- Partner-facing report changes beyond the existing aggregate pack.
- Changes to consent policy or privacy approval workflow.

## Acceptance Criteria

- [x] Authenticated activity events are accepted only for the current user and resolved through existing cohort consent rules.
- [x] A cohort member generates at most one daily activity event per UTC day.
- [x] Activity metadata contains no route, property, document, chat or free-text content.
- [x] The report exposes `repeatActiveMembers` and a repeat-use rate calculated from at least two distinct UTC activity dates.
- [x] Anonymous invite-view tracking remains available before login and cannot impersonate an authenticated member.
- [x] Focused automated verification and representative-data smoke pass.
- [x] HT-324, HT-322 and HT-320 reflect the resulting metric coverage.

## Review / Decision Gate

This ticket is technically complete when the metric is accurate and aggregate-only. Product/pilot and privacy/compliance approval of the external reporting pack remain separate launch decisions.

## Implementation Log

### 2026-08-02
- Repo: backend, frontend, docs, tickets
- Changed:
  - backend PR #4 adds an authenticated `/api/partner-onboarding/activity` endpoint, daily uniqueness migration and aggregate repeat-use metric
  - frontend PR #2 emits the activity signal once per signed-in user per UTC day, without contextual metadata
  - public invite-view tracking remains before authentication
- Verification:
  - backend syntax checks and focused reporting verifier pass
  - local migration `20260802110000-add-pilot-event-activity-date` applied successfully
  - representative two-member MySQL smoke passed: same-day call deduplicated, two UTC dates produced one repeat member and a 50% repeat-use rate, then all fixtures were removed
  - frontend production build passes with the existing unrelated lint warnings in `KnowledgeBaseAdmin.jsx` and `DataPrivacySettings.jsx`
- Notes: implementation is awaiting the code review loop in backend PR #4 and frontend PR #2. Target-environment smoke, product/pilot interpretation and privacy/compliance acceptance remain separate launch work.
