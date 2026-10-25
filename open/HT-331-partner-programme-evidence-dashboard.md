# HT-331: Build the partner programme evidence dashboard

**Priority:** P1
**Repo:** backend / frontend / docs
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-10-25

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

## Delivery Contract — 2026-10-25

HT-332 merged in backend PR #7 and frontend PR #5. Build from those merged main heads.

### Implementation Workstreams

1. Add a partner-only report service using HT-332 server-side authorization; never expose the admin cohort report through a partner route.
2. Return distinct eligible participant metrics for activation, setup, documents, tasks, property-aware questions, repeat use and feedback participation. Do not export feedback content or ratings.
3. Restrict reports to fixed, non-overlapping calendar months and programme/campaign partitions. Reject arbitrary date windows and unknown query keys. Report only campaign partitions: no programme-total rollup that could reconstruct a suppressed campaign.
4. Require current granted processing, analytics and partner-reporting consent bound to the same member, cohort, partner and user. Exclude withdrawn/removed members and historical activity after consent withdrawal. Never return participant or property identifiers.
5. Require at least ten eligible participants per partition. Suppress metric values and rates when either the numerator or its complement is between one and four. Empty and suppressed partitions return no participant totals. Definitions and coverage explain every output.
6. Add programme/campaign/month selection, clear suppressed/no-data/approval/denied states and a JSON aggregate review-pack export to the existing governed workspace. Privacy auditors can read definitions, not metrics or exports.
7. Keep runtime reporting disabled by default. Enable only specific programme IDs through deployment configuration after HT-324 product/privacy approval; configuration is an operational gate, not evidence of that approval.

### Verification Required

- Backend policy and response-contract verifier: scope, roles, invalid filters, consent exclusion, small partitions, numerator/complement suppression, fixed months and exports.
- Real local MySQL fixture smoke with cleanup, including consent withdrawal and cross-programme denial.
- Existing access, acquisition, lifecycle and pilot-reporting verifiers.
- Frontend tests for report, suppression, error, definitions and export; build, changed-file lint and exact-head browser/mobile smoke.
- Complete base-to-feature review/fix loop, CI and accurate PR evidence.

### Scope Decisions And Remaining Launch Gates

- No arbitrary sliding windows, programme-total rollups, individual data, feedback text/ratings or regulated-outcome claims. Metrics measure recorded engagement only.
- HT-324 product/pilot interpretation and privacy approval remain outstanding. Default-off reporting preserves that boundary while implementation and fixture validation proceed.
- HT-319 consent/deletion governance and HT-320 target-environment rehearsal remain launch requirements.
