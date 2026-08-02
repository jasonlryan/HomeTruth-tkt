# HT-329: Build controlled partner-programme lifecycle administration

**Priority:** P1
**Repo:** backend / frontend
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-08-02

## Goal

Let a HomeTruth operator configure and manage a repeatable partner programme without code changes for each partner or cohort.

## Objective

Extend the existing partner/cohort model with a controlled programme lifecycle: programme status, cohort dates, entitlement, approved campaign route, invite configuration and closure/suspension state.

## Scope

- Operator-only programme configuration initially.
- Shared configuration for insurers, mortgage providers, home developers and other B2B clients; partner type changes labels and pack selection, not the lifecycle or access model.
- Partner, programme, cohort and campaign lifecycle states.
- Invite mode, cohort keys, dates, entitlement and approved content references.
- Audit fields for creation, change, suspension and closure.
- Safe migration of existing partner/cohort data.

## Out Of Scope

- Partner self-service administration.
- SSO, CRM integrations or external APIs.
- Individual homeowner data access.
- Building vertical-specific workflows.

## Implementation Workstreams

1. **Shared persistence:** add programme and campaign records, link existing cohorts safely, and retain the current partner/cohort/member/consent contracts.
2. **Lifecycle service and API:** expose admin-only create, list, update and transition operations with explicit valid transitions and audit evidence.
3. **Operator UI:** let a HomeTruth administrator configure a partner programme and initial cohort/campaign, inspect status and perform valid lifecycle actions.
4. **Compatibility and privacy:** prove insurer, mortgage-provider, home-developer and other partner types use the same programme contract and that no individual homeowner data is returned or granted.

## Acceptance Criteria

- [x] A programme can be created for an existing or new partner without code changes.
- [x] A programme supports status, owner, cohort, dates, entitlement, invite mode and approved content references.
- [x] An operator can activate, pause and close a programme with audit metadata.
- [x] Existing cohort membership and consent behaviour remains compatible.
- [x] Configuration does not grant the partner access to individual homeowner data.
- [x] Insurer, mortgage-provider, home-developer and other partner types use the same programme lifecycle schema, service and API.
- [x] API and UI validation cover invalid lifecycle transitions and unauthorized access.
- [x] A feature branch, PR and clean review loop are completed.

## Dependencies

- HT-328 scope gate accepted.
- HT-314 partner/cohort/consent model.

## Review Gate

Confirm whether operator-only configuration is sufficient for the first B2B deal before adding partner self-service.

Decision recorded 2026-08-02:

- Build the shared operator-only lifecycle first, consistent with the active B2B2C scope and Phase 1 pilot-kit boundary.
- Do not wait for a named partner and do not introduce partner self-service, SSO or integration work in HT-329.
- Treat insurer as one supported partner type and future reference pack, not as the programme schema default or a special lifecycle path.
- Governed partner roles and any partner-facing access remain HT-332; HT-329 admin responses must exclude members, users, properties, documents, tasks, consent records and behavioural event rows.

## Required Verification

- Record migration status before and after applying the HT-329 migration; verify rollback and re-apply when the local dependency path supports it.
- Run syntax checks for every changed backend JavaScript file and `git diff --check` in each implementation repository.
- Add a focused lifecycle verifier covering creation for every supported partner type, list/detail output, valid and invalid transitions, audit events, admin authorization and response-field privacy.
- Run the existing pilot-reporting verifier and confirm existing invite validation still loads against the migrated models.
- Run the frontend production build and focused UI tests.
- Browser-smoke the exact frontend feature head for programme creation, lifecycle actions, validation/error states and narrow/mobile layout using mocked or local APIs tied to that head.
- Complete the base-branch review/fix loop and record PR URLs, base/head SHAs, final local gates, CI, mergeability and remaining target-environment gaps before closure.

## Implementation Evidence

Implemented 2026-08-02 on the shared feature branch `feature/ht-329-partner-programme-lifecycle` in each implementation repository.

- Backend: added shared partner-programme, campaign and audit-event persistence; safe links to existing cohorts; admin-only create/list/update/transition APIs; lifecycle transition and activation guards; configured invite-mode enforcement; child campaign/cohort state propagation; before/after audit evidence; and aggregate-only response shaping.
- Frontend: added an operator Partner Programmes workspace for creating a new or existing partner's programme, campaign and cohort; lifecycle actions; shared insurer, mortgage-provider, home-developer and other-B2B-client configuration; accessible validation; responsive presentation; and discovery from the existing admin hub.
- Privacy boundary: no programme response or operator screen exposes partner members, homeowner/user records, properties, documents, tasks, consents or behavioural event rows.

## Pull Requests And Review

- Backend PR: https://github.com/jasonlryan/HomeTruth-be/pull/5
  - Base: `main` at `0b5a16492ac72927895e5b0008bf0bbaeb1f457c`
  - Head: `567f7a6a96e3629faf1efe9c68db4baa39110960`
- Frontend PR: https://github.com/jasonlryan/HomeTruth-fe/pull/3
  - Base: `main` at `2c0ccab1d323f8413309fb450e7fc48a907dd8b5`
  - Head: `af17ccc0026dabcc252aac580a0cff900a4e8c2f`
- The first full three-dot base review found four actionable issues: configured invite modes were not enforced, unexpected backend errors could expose implementation details, update audit records lacked before/after state, and the operator page was not discoverable from the admin hub.
- All four findings were fixed on the existing feature branches. Focus and accessible error-state handling were strengthened in the same review pass, and the MySQL smoke test gained positive and negative invite-mode coverage.
- A repeated full three-dot review from the clean `main` worktrees found no remaining actionable issues.
- Both existing PRs were moved from draft to ready exactly once after the final local gate. Each contains its current base, is fully pushed, `MERGEABLE` with a `CLEAN` merge state, and has no open review comments.

## Verification Evidence

Backend final gate at `567f7a6a96e3629faf1efe9c68db4baa39110960`:

- Recorded the new migration as down, applied it, verified a repaired rollback after detecting a MySQL foreign-key/index ordering issue, and re-applied it successfully. Final local migration status is `up` for `20260802130000-create-partner-programme-lifecycle.js`.
- `node --check` passed for every changed backend JavaScript file.
- `node scripts/verifyPartnerProgrammeLifecycle.js` passed creation, shared-type compatibility, lifecycle, audit, authorization and response-privacy checks.
- `node scripts/verifyPilotReportingCoverage.js` passed, retaining the existing pilot reporting contract.
- `node scripts/smokePartnerProgrammeLifecycle.js` passed against local MySQL with fixture cleanup for insurer, mortgage provider, home developer and other B2B clients, including enabled and disabled invite routes.
- `git diff --check origin/main...HEAD` passed.

Frontend final gate at `af17ccc0026dabcc252aac580a0cff900a4e8c2f`:

- Focused programme utility tests passed: 1 suite, 3 tests.
- Production build passed. It reported only the existing unused-handler warnings in `KnowledgeBaseAdmin.jsx` and `DataPrivacySettings.jsx` plus the repository's existing Browserslist/bundle-size notices.
- Changed-file ESLint passed with zero errors; the existing `KnowledgeBaseAdmin.jsx` unused-handler warning remains.
- Exact-head browser verification passed for admin-hub discovery, creation of an `other` B2B client programme, mortgage-provider activation with child campaign state propagation, empty-form validation and first-invalid-field focus, accessible invalid states, aggregate-only copy and a 390-by-844 mobile viewport. The browser console contained only the React development-tools informational message.
- `git diff --check origin/main...HEAD` passed.

CI and PR state on 2026-08-02:

- GitGuardian Security Checks passed on both exact PR heads.
- These PRs expose no repository-specific GitHub Actions build or test workflow beyond the configured GitGuardian check; the build, tests, migration checks, MySQL smoke and browser gate above are the final implementation gates.

## Current Status And Remaining Gaps

- HT-329 is clear to merge but remains open until both implementation PRs are merged and the post-merge branch/worktree verification is recorded.
- No target deployment or production data migration was performed in this workstream.
- Partner self-service, SSO, CRM/external integrations, governed partner roles and any individual-data sharing remain out of scope and are governed by later HT-328 workstreams, including HT-332.
