# HT-331: Build the partner programme evidence dashboard

**Priority:** P1
**Repo:** backend / frontend / docs
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-08-02

## Goal

Enable a partner sponsor and programme manager to assess programme value through clear, privacy-protected aggregate evidence.

## Objective

Turn the pilot reporting foundation into a repeatable programme dashboard with agreed metric definitions, thresholding, consent-aware filtering and decision-ready exports.

## Scope

- Aggregate activation, property setup, document linking, task engagement, property-aware questions, repeat use and feedback metrics.
- Programme/campaign/date filters within the approved access boundary.
- Minimum cohort thresholds and suppression behaviour.
- Metric coverage, definitions, consent basis and no-data explanation.
- Decision-ready aggregate export or shareable review pack.

## Out Of Scope

- Individual homeowner, property, document, task or chat views.
- Claims, credit, underwriting or valuation decisions.
- Metrics that are not instrumented or cannot be explained.

## Acceptance Criteria

- [ ] Approved partner roles can view only aggregate data for their permitted programmes.
- [ ] Reports suppress small cohorts and exclude identifying or sensitive fields.
- [ ] Every displayed metric has a source, definition and coverage state.
- [ ] Consent withdrawal affects reporting according to the approved policy.
- [ ] The dashboard supports a renewal, expansion or stop decision without manual data assembly.
- [ ] Privacy, authorization and report-response tests pass.
- [ ] A feature branch, PR and clean review loop are completed.

## Dependencies

- HT-328 scope gate accepted.
- HT-324 reporting/privacy validation.
- HT-326 repeat-use instrumentation.
- HT-332 governed partner access controls.
