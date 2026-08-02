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
- Partner, programme, cohort and campaign lifecycle states.
- Invite mode, cohort keys, dates, entitlement and approved content references.
- Audit fields for creation, change, suspension and closure.
- Safe migration of existing partner/cohort data.

## Out Of Scope

- Partner self-service administration.
- SSO, CRM integrations or external APIs.
- Individual homeowner data access.
- Building vertical-specific workflows.

## Acceptance Criteria

- [ ] A programme can be created for an existing or new partner without code changes.
- [ ] A programme supports status, owner, cohort, dates, entitlement, invite mode and approved content references.
- [ ] An operator can activate, pause and close a programme with audit metadata.
- [ ] Existing cohort membership and consent behaviour remains compatible.
- [ ] Configuration does not grant the partner access to individual homeowner data.
- [ ] API and UI validation cover invalid lifecycle transitions and unauthorized access.
- [ ] A feature branch, PR and clean review loop are completed.

## Dependencies

- HT-328 scope gate accepted.
- HT-314 partner/cohort/consent model.

## Review Gate

Confirm whether operator-only configuration is sufficient for the first B2B deal before adding partner self-service.
