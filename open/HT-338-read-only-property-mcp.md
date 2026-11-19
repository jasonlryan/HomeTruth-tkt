# HT-338: Build the read-only property MCP service

**Priority:** P1
**Repo:** backend / frontend / docs
**Created:** 2026-10-25
**Status:** Planned, not implemented

## Objective

Expose a small, bounded tool interface over authorised HomeTruth property services with sources and explicit uncertainty.

## Scope

Property listing/summary, known dates, available service evidence, curated guidance and controlled evidence retrieval; observability/rate limits.

## Out Of Scope

Writes, booking, payments, scheduled monitoring and invented property facts or dates.

## Implementation Workstreams

1. Agree and record the bounded contract and unresolved external decisions.
2. Implement on a ticket-named feature branch only after its contract is accepted.
3. Complete focused and dependency-path validation, base-branch review/fixes and one PR per implementation repository.

## Acceptance Criteria

- [ ] HT-336 data contract and HT-337 authorisation are respected.
- [ ] Tool schemas, limits, sources and errors are documented.
- [ ] Documents cannot override instructions or permissions.
- [ ] Permissioned evidence links and unavailable/unknown states work.

## Required Verification

Real service-path integration; second-user isolation; revoked grants; prompt injection; source integrity; timeouts/retries; full feature PR loop.

## Dependencies And Decisions

HT-335 plan: `hometruth DOCS/docs/product/personal-agent-opda-delivery-plan.md`. Follow the workstream sequence and external approval gates there. No technical owner, budget or delivery date is assumed.

## HT-FLOW-005 database requirements

**Reuse.** Read dated tasks and facts from `property_tasks` and `property_facts`. Resolve citations through `property_documents` and `evidence_sources`.

**Missing or required.** The local schema has no dedicated maintenance-event or compliance record. Report missing dates as unknown. Each fact currently references one evidence source. A claim reconciled across several documents needs a way to retain all supporting sources.

**Decision needed.** Which dated records support the first pilot answer? Do we need multi-source claims or a dedicated event model for that pilot?

This records planning requirements only. Connect your agent remains on the roadmap.
