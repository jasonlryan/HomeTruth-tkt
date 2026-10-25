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

## Implementation And Review Evidence — 2026-10-25

- Backend PR: https://github.com/jasonlryan/HomeTruth-be/pull/8
  - Base `main`: `b848518d3cb0bbb4fbe165656c09a07f093ec7ac`.
  - Reviewed feature head: `5786bbaefa8997a038b8561446877771c5f11944`.
- Frontend PR: https://github.com/jasonlryan/HomeTruth-fe/pull/6
  - Base `main`: `707e18fbf67f3ea68209820bf4a8622c77494b34`.
  - Final head is recorded in the final gate entry below.
- Contract: `hometruth DOCS/docs/product/partner-programme-evidence-contract.md`, documentation commit `744cba5`.
- Code and fixes are exclusively on `feature/ht-331-partner-evidence` in each implementation repository. No implementation changes were made directly on main.

### Delivered

- Scoped monthly campaign evidence and JSON export; no programme-total rollups or individual rows.
- Current processing/analytics/reporting consent, exact member/user/cohort/partner matching, withdrawn-member exclusion and duplicate-enrolment exclusion.
- Minimum group 10; non-zero numerators and complements below 5 suppressed with null counts/rates.
- Eight defined engagement measures with sources, denominator, units and instrumented coverage. Feedback content and ratings excluded.
- Active reporting roles can load evidence; privacy auditors see definitions only. Programme-specific default-off deployment gate preserves outstanding HT-324 approval.
- Detects calculation-time changes in access, consent, membership, partner reporting mode, campaign scope and cohort reporting settings.
- Existing schema reused; no new migration. Capacity fails closed above 100,000 member, consent or event rows.

### Base-Branch Review And Fixes

- Backend reviewed from clean `HomeTruth_BE-staging` on main; frontend reviewed from clean `HT_Frontend-review-main` on main. Existing unrelated frontend-main asset deletions were preserved in `HT_Frontend-staging`.
- Complete three-dot diffs and surrounding authorization, consent, event and workspace callers inspected.
- Fixed audit definition events to match the existing database enum.
- Excluded ambiguous duplicate memberships to prevent inflated and overlapping campaign populations.
- Added final consent/membership/scope and reporting-mode rechecks; real-MySQL regressions simulate consent withdrawal and cohort reporting changes during event retrieval.
- Corrected browser fixture denial responses to use the existing Axios error helper.
- Repeated review found no remaining actionable feature findings.

### Verification

- Backend syntax checks and full diff whitespace checks passed.
- New evidence contract verifier and existing access, acquisition, lifecycle and pilot-reporting verifiers passed.
- Real local MySQL evidence smoke passed across all four partner types and three reporting roles, auditor definition-only access, approval gate, scoped campaign filters, duplicate enrolments, consent withdrawal, calculation-time changes, lifecycle/revoke denial, export audit and privacy-safe output. Fixtures cleaned up.
- Existing access, acquisition and lifecycle MySQL smokes passed. Docker and the existing hometruth-mysql container were started for these checks.
- Frontend applicable suites: 4 suites, 16 tests passed, including protected cells, stale-filter clearing, denial, approval states, auditor restrictions and fresh export authorization.
- Full frontend suite has a pre-existing `src/App.test.js` failure: Jest cannot resolve react-router-dom. Reproduced unchanged on main with the existing dependencies. This is not a passing full-suite claim and is outside this feature's repair scope.
- Production build passed; changed-file lint passed. Existing two unrelated unused-variable warnings, Browserslist age and bundle-size notices remain.
- Isolated visual-review browser at port 3011 served the frontend feature worktree, verified through the server process cwd. Browser checked monthly evidence, protected cells, successful JSON download, denied access, suppressed/no-data/approval states and privacy-auditor definitions only. 390px evidence layout visually inspected; desktop horizontal-overflow check passed. Browser uses fixture APIs; live backend behavior is evidenced by MySQL smoke, not an end-to-end target deployment.

### Remaining Boundaries

- PRs remain unmerged; HT-331 remains open pending integration.
- HT-324 product/pilot interpretation and privacy approval, HT-319 governance and HT-320 target-environment rehearsal remain outstanding. No production programme was enabled.
- Threshold policy, repeated-download disclosure risks and the intentionally different monthly engagement denominators require approval before external sharing.
