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

- [ ] A programme can be created for an existing or new partner without code changes.
- [ ] A programme supports status, owner, cohort, dates, entitlement, invite mode and approved content references.
- [ ] An operator can activate, pause and close a programme with audit metadata.
- [ ] Existing cohort membership and consent behaviour remains compatible.
- [ ] Configuration does not grant the partner access to individual homeowner data.
- [ ] Insurer, mortgage-provider, home-developer and other partner types use the same programme lifecycle schema, service and API.
- [ ] API and UI validation cover invalid lifecycle transitions and unauthorized access.
- [ ] A feature branch, PR and clean review loop are completed.

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
