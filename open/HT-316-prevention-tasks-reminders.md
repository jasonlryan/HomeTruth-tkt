# HT-316: Build prevention tasks and reminders

**Priority:** P1
**Repo:** both
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Give users useful home-prevention actions based on their property profile, documents and facts.

## Description

The homeowner proposition depends on HomeTruth helping people catch small home issues early and keep their property record useful. For partner cohorts, this may create downstream aggregate pilot signals, but the product experience must be homeowner-first.

This ticket creates the first prevention task/reminder capability: generate, display and track actions such as boiler service, gutter checks, damp follow-up, document expiry and seasonal maintenance.

The first version should be rules-led and evidence-aware. It should not depend on speculative AI autonomy.

## Dependencies

- HT-313: property facts and evidence layer
- HT-315: insurer invite and onboarding
- Docs: `hometruth DOCS/docs/product/homeowner-first-prevention-and-partner-access.md`

## Expected Files

- `HomeTruth_BE-staging/migrations/...create-property-tasks.js`
- `HomeTruth_BE-staging/models/propertyTask.js`
- `HomeTruth_BE-staging/services/preventionTaskService.js`
- `HomeTruth_BE-staging/routes/propertyTaskRoutes.js`
- `HT_Frontend-staging/src/...` task/reminder UI
- `HomeTruth-tickets/open/HT-316-prevention-tasks-reminders.md`

## Acceptance Criteria

- [ ] Backend stores prevention tasks with property, assignee, source, status, due date and completion state.
- [ ] Initial rules generate tasks from property facts, evidence, document expiry dates or missing baseline data.
- [ ] Tasks can be listed on a property profile.
- [ ] User can mark a task complete, dismissed or not relevant.
- [ ] Task status changes are tracked for pilot analytics.
- [ ] UI displays tasks clearly and uses HomeTruth design-system tokens.
- [ ] No insurer claim-reduction claims are shown in-product unless supported by approved copy.
- [ ] No partner-facing individual task view or task-control capability is introduced in HT-316.
- [ ] HT-316 remains pull-led with light in-app prompts only; no email, SMS, partner-app push or insurer-triggered nudges.
- [ ] Verification covers task generation, task listing, status update and UI smoke test.
- [ ] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review the prevention taxonomy before implementation. Key decision: which tasks are safe and useful for homeowners in the first 500-person cohort, and which require insurer/legal review.

## Decision Log / Return To

- 2026-05-30: HT-316 is homeowner-usefulness first. It is not an insurer compliance checklist.
- 2026-05-30: First version is pull-led with light in-app prompts only. External push is deferred.
- 2026-05-30: The insurer is a partner/cohort actor, not a `PropertyPerson` by default.
- 2026-05-30: The partner gets no default access to property documents, raw facts, task status, personal profiles or individual report data without explicit future consent.
- 2026-05-30: Documented governance in `hometruth DOCS/docs/product/homeowner-first-prevention-and-partner-access.md`.
- Return to: notification channels, notification frequency, partner aggregate analytics, explicit report-sharing consent, and any prevention categories needing legal/regulatory review.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-316 for prevention tasks and reminders.
- Verification: roadmap planning only.
- Notes: first version should be rules-led, measurable and conservative.

### 2026-05-30
- Repo: docs, tickets
- Changed: documented homeowner-first prevention and partner access governance before implementation; updated HT-316 goal, AC and decision log.
- Verification: documentation review only.
- Notes: implementation must keep insurer/partner access out of individual task control and individual property data by default.
