# HT-319: Define data deletion and consent withdrawal runbook

**Priority:** P1
**Repo:** docs / tickets
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-30
**Updated:** 2026-05-31

## Goal

Define the operational process for consent withdrawal, data deletion and partner reporting implications before pilot launch.

## Description

The platform now records partner cohort consent, property records, documents, facts, prevention tasks and aggregate pilot events. Before a live partner cohort, HomeTruth needs a clear runbook for what happens when a user withdraws consent or requests deletion.

This ticket is operational and governance-focused. It should not add destructive automation until the process is reviewed.

## Dependencies

- HT-314: partner cohort and consent model
- HT-317: pilot analytics, reporting and readiness review

## Expected Files

- `hometruth DOCS/docs/product/data-deletion-consent-withdrawal-runbook.md`
- `HomeTruth-tickets/open/HT-319-data-deletion-consent-withdrawal-runbook.md`

## Acceptance Criteria

- [x] Withdrawal path is defined for each consent scope: `hometruth_processing`, `partner_reporting`, `aggregate_analytics`, `individual_report_access`, `partner_contact_servicing`.
- [x] Deletion/anonymisation implications are mapped for users, cohort members, consent records, property records, documents, facts, tasks and pilot events.
- [x] Process states are defined: requested, verified, in progress, completed, rejected, escalated.
- [ ] Identity verification requirement is documented.
- [ ] Target handling time and escalation rule are documented.
- [x] Partner-reporting impact is documented without exposing personal data.
- [x] Manual DB/admin steps are explicitly listed or deferred to a follow-up tooling ticket.
- [ ] Legal/privacy review requirement is recorded.
- [ ] Runbook is reviewed and accepted before pilot launch.

## Review / Decision Gate

This cannot be completed without privacy/legal confirmation. Key decision: what data is deleted versus retained/anonymised for audit, safety and legal obligations.

## Implementation Log

### 2026-05-30
- Repo: tickets
- Changed: created HT-319 from HT-317 launch blockers.
- Verification: ticket derived from completed HT-317 readiness review and HT-314 consent model.
- Notes: do not implement destructive deletion automation before the runbook is accepted.

### 2026-05-31
- Repo: docs, tickets
- Changed:
  - `hometruth DOCS/docs/product/data-deletion-consent-withdrawal-runbook.md`
  - `HomeTruth-tickets/open/HT-319-data-deletion-consent-withdrawal-runbook.md`
- Verification: drafted consent-scope withdrawal behaviour, delete/anonymise object map, Qdrant implications, process states, partner-reporting impact and manual checklist.
- Notes: still blocked on privacy/legal owner, identity verification route, target handling time, escalation owner and delete-versus-anonymise policy approval.

### 2026-08-02
- Repo: docs, tickets
- Changed: Jason Ryan is recorded as interim privacy operations and escalation owner.
- Verification: owner assignment supplied directly by the pilot owner.
- Notes: this permits operational preparation, but external legal/privacy review, identity verification, handling time and delete-versus-anonymise policy approval remain open decisions.
