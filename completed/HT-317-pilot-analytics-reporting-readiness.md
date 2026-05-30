# HT-317: Build pilot analytics, reporting and readiness review

**Priority:** P1
**Repo:** both
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-30

## Goal

Make the 500-user insurer pilot measurable, reportable and operationally reviewable before launch.

## Description

The pilot must produce evidence, not just usage. HomeTruth needs analytics and reporting that show activation, property setup, document linking, fact capture, prevention tasks, engagement and user feedback while respecting consent boundaries.

This ticket also acts as the launch-readiness review for the insurer cohort.

## Dependencies

- HT-314: partner cohort and consent model
- HT-315: insurer invite and onboarding
- HT-316: prevention tasks and reminders

## Expected Files

- `HomeTruth_BE-staging/migrations/...create-pilot-events.js`
- `HomeTruth_BE-staging/models/pilotEvent.js`
- `HomeTruth_BE-staging/services/pilotAnalyticsService.js`
- `HomeTruth_BE-staging/routes/admin/...`
- `HT_Frontend-staging/src/...` admin/reporting surface if in scope
- `HomeTruth-tickets/completed/HT-317-pilot-analytics-reporting-readiness.md`

## Acceptance Criteria

- [x] Pilot events are captured for invite, signup, consent, property setup, document link, fact creation, task generation, task completion and user feedback.
- [x] Events include partner/cohort context where consent allows it.
- [x] Admin/reporting endpoint returns cohort-level metrics without exposing unnecessary personal data.
- [x] Report covers activation, completion, engagement, prevention-task actions and drop-off points.
- [x] Data sharing boundaries match the consent model from HT-314.
- [x] Operational readiness checklist exists for support, monitoring, failed onboarding, data deletion and incident handling.
- [x] Pilot go/no-go review records open risks and launch blockers.
- [x] Verification covers event capture, aggregate reporting and consent-boundary checks.
- [x] Implementation log records changed files and verification performed.

## Review / Decision Gate

Final pilot readiness review. Key decision: whether the platform is ready for a 500-user insurer cohort, or whether launch must wait for specific blockers.

Decision recorded 2026-05-30:

- Technical event capture and aggregate pilot reporting are in place.
- Launch recommendation remains `no_go` until operational blockers are closed.
- Current blockers:
  - assign support owner and escalation contact
  - confirm incident response path
  - confirm data deletion / withdrawal runbook
  - review production cohort invite setup before launch

## Event Taxonomy V1

Durable pilot events should use these names:

- `invite_viewed`
- `signup_completed`
- `consent_recorded`
- `property_setup_completed`
- `document_linked`
- `fact_created`
- `tasks_generated`
- `task_completed`
- `task_dismissed`
- `task_not_relevant`
- `user_feedback_submitted`

Each event should carry:

- event category
- source type/model/id
- user and property ids for internal operational traceability
- partner/cohort/member ids only where the consent and context boundary allows it
- metadata with counts, task type, fact key or feedback rating where useful

## Reporting Boundary V1

Admin reporting for HT-317 is cohort-level only. It must not return user rows, names, emails, property addresses, document names, raw facts, task descriptions or individual member status.

Partner/cohort context is allowed when:

- the event is anonymous invite activity with no user/property data; or
- the user has granted `aggregate_analytics` consent for the cohort/member context.

If aggregate consent is missing or withdrawn, internal product events can still be recorded for operational integrity, but partner/cohort fields should not be attached to the event.

## Operational Readiness Checklist V1

- Support owner and escalation path identified.
- Failed invite/onboarding states visible in aggregate.
- Data deletion/withdrawal path documented before launch.
- Incident contact path documented before launch.
- Cohort reporting reviewed for privacy leakage.
- Notification/push scope explicitly excluded from V1.
- Go/no-go decision recorded with launch blockers.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-317 for pilot analytics, reporting and readiness review.
- Verification: roadmap planning only.
- Notes: this is the final review gate before any insurer cohort launch.

### 2026-05-30
- Repo: tickets
- Changed: defined V1 pilot event taxonomy, reporting boundary and operational readiness checklist before implementation.
- Verification: reviewed against HT-314 consent model and homeowner-first/aggregate-only governance.
- Notes: partner/cohort context is attached only for anonymous invite activity or where `aggregate_analytics` consent allows it.

### 2026-05-30
- Repo: backend
- Changed:
  - `HomeTruth_BE-staging/migrations/20260530170000-create-pilot-events.js`
  - `HomeTruth_BE-staging/models/pilotEvent.js`
  - `HomeTruth_BE-staging/services/pilotAnalyticsService.js`
  - `HomeTruth_BE-staging/Controllers/admin/adminPilotController.js`
  - `HomeTruth_BE-staging/Controllers/pilotFeedbackController.js`
  - `HomeTruth_BE-staging/routes/admin/adminPilotRoutes.js`
  - `HomeTruth_BE-staging/routes/pilotFeedbackRoutes.js`
  - `HomeTruth_BE-staging/services/partnerOnboardingService.js`
  - `HomeTruth_BE-staging/services/propertyDocumentService.js`
  - `HomeTruth_BE-staging/services/propertyFactService.js`
  - `HomeTruth_BE-staging/services/propertyTaskService.js`
  - `HomeTruth_BE-staging/models/index.js`
  - `HomeTruth_BE-staging/server.js`
- Verification:
  - `node --check` passed for new/changed backend services, controllers, routes, model and migration.
  - `git diff --check` passed.
  - `npm run db:migrate` applied `20260530170000-create-pilot-events.js`.
  - `npm run db:migrate:status` shows all current migrations up.
  - Route load check passed for pilot admin, feedback and onboarding routes.
  - Direct local MySQL verification passed for event before consent not attaching partner context, event after aggregate consent attaching cohort context, feedback aggregation, and aggregate report excluding personal row fields.
- Notes: admin report returns cohort-level metrics only; no user, member, property, document or raw fact rows are returned.

### 2026-05-30
- Repo: frontend
- Changed:
  - `HT_Frontend-staging/src/api/api.js`
  - `HT_Frontend-staging/src/pages/AdminReportingDashboard.jsx`
  - `HT_Frontend-staging/src/dev/VisualReviewHarness.jsx`
  - `HT_Frontend-staging/src/pages/PartnerOnboarding.jsx`
  - `HT_Frontend-staging/src/pages/PropertyProfile.jsx`
- Verification:
  - `npm run build` passed with pre-existing unused-var and Browserslist warnings.
  - `git diff --check` passed.
  - Browser smoke passed at `/visual-review/admin?to=/admin/dashboard`: pilot readiness panel rendered aggregate privacy boundary and `no_go` recommendation.
- Notes: consent/property completion events are now captured server-side; frontend keeps only lightweight invite viewed and property started emits.
