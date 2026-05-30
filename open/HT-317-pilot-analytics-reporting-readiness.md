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
- `HomeTruth-tickets/open/HT-317-pilot-analytics-reporting-readiness.md`

## Acceptance Criteria

- [ ] Pilot events are captured for invite, signup, consent, property setup, document link, fact creation, task generation, task completion and user feedback.
- [ ] Events include partner/cohort context where consent allows it.
- [ ] Admin/reporting endpoint returns cohort-level metrics without exposing unnecessary personal data.
- [ ] Report covers activation, completion, engagement, prevention-task actions and drop-off points.
- [ ] Data sharing boundaries match the consent model from HT-314.
- [ ] Operational readiness checklist exists for support, monitoring, failed onboarding, data deletion and incident handling.
- [ ] Pilot go/no-go review records open risks and launch blockers.
- [ ] Verification covers event capture, aggregate reporting and consent-boundary checks.
- [ ] Implementation log records changed files and verification performed.

## Review / Decision Gate

Final pilot readiness review. Key decision: whether the platform is ready for a 500-user insurer cohort, or whether launch must wait for specific blockers.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-317 for pilot analytics, reporting and readiness review.
- Verification: roadmap planning only.
- Notes: this is the final review gate before any insurer cohort launch.
