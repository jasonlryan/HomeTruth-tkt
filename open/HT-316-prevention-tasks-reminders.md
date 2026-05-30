# HT-316: Build prevention tasks and reminders

**Priority:** P1
**Repo:** both
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Give insurer-cohort users useful prevention actions based on their property profile, documents and facts.

## Description

The insurer proposition depends on HomeTruth helping homeowners catch small problems early. This ticket creates the first prevention task/reminder capability: generate, display and track actions such as boiler service, gutter checks, damp follow-up, document expiry and seasonal maintenance.

The first version should be rules-led and evidence-aware. It should not depend on speculative AI autonomy.

## Dependencies

- HT-313: property facts and evidence layer
- HT-315: insurer invite and onboarding

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
- [ ] Verification covers task generation, task listing, status update and UI smoke test.
- [ ] Implementation log records changed files and verification performed.

## Review / Decision Gate

Review the prevention taxonomy before implementation. Key decision: which tasks are safe and useful for the first 500-person cohort, and which require insurer/legal review.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-316 for prevention tasks and reminders.
- Verification: roadmap planning only.
- Notes: first version should be rules-led, measurable and conservative.
