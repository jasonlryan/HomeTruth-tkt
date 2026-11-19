# HT-351: Persist run revisions and enforce execution limits

**Repo:** backend
**Priority:** P1
**Created:** 2026-11-19
**Depends on:** HT-350
**Specification:** HomeTruth product docs, `docs/product/agent-sdk-integration.md` (2992cdc).

## Goal

Make retry, recovery and rollout safe across revisions and concurrent backend instances.

## Implementation

Record the resolved revision, operation, fingerprint, resource, timings and usage. Add enabled-revision selection, a disable switch, principal-level concurrency and cost budgets, and conditional terminal transitions. Validate registry settings and tool capabilities before serving.

## Scope boundary

Retention and child messaging have separate tickets.

## Acceptance criteria

- [ ] Concurrent identical requests reserve once.
- [ ] Conflicting reuse fails.
- [ ] Disabled agents reject new runs while historical results can be read.
- [ ] Legacy appliance rows resolve to a compatible reader.
- [ ] Timeout and access loss release reservations.

## Verification

Exercise competing workers, revocation, failed writes, configured limits and revision rollback with a real database and a stub provider.

## HT-FLOW-005 database requirements

**Reuse.** Extend the existing `appliance_agent_runs` record and its request-key handling for the initial specialist.

**Missing or required.** Bind a run to its initiating user, selected resource, operation, revision and input fingerprint. Retain state and usage so repeat clicks reuse the same result and changed inputs under the same key are rejected.

**Approved UK pilot, 19 November 2026.** One concurrent paid manual lookup per homeowner. Reserve £0.20 per fresh paid attempt against a £1.00 daily allowance (UTC). Identical retries reuse the existing result. The GBP profile is approved for pilot enablement. EUR and USD profiles remain inactive. Keep one balance and currency per homeowner per day, including across homes. HomeTruth funds the pilot; these allocations create no customer charge or subscription debit.

**Implementation and verification.** [Backend PR #14](https://github.com/jasonlryan/HomeTruth-be/pull/14), commit `442fee1`, separates market-currency reservations from internal USD provider estimates (model input, cached input, output and hosted web search). Missing provider data may leave an estimate unknown or partial. No production migration or rollout was performed. All 29 offline tests and isolated MySQL checks passed, including five admissions, sixth denial, replay, inactive markets, currency pinning and legacy USD handling.

This records planning requirements only. Connect your agent remains on the roadmap.
