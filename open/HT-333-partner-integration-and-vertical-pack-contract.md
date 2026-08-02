# HT-333: Define partner integration and vertical-pack contracts

**Priority:** P2
**Repo:** backend / docs / tickets
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-08-02

## Goal

Make future partner integrations and segment-specific features additive to the shared programme model rather than bespoke forks.

## Objective

Define stable integration and configuration contracts for partner identifiers, invite handoff, programme status, consent-safe aggregate reporting and vertical content packs.

## Scope

- Opaque external identifier and correlation rules.
- Supported invite and attribution handoff patterns.
- Aggregate reporting/export contract.
- Versioned configuration model for document prompts, task rules, copy and success measures.
- Compatibility rules for insurer, mortgage-provider and new-build packs.

## Out Of Scope

- Building a CRM, SSO, API or webhook integration without a committed partner requirement.
- Passing individual homeowner data through an integration by default.
- Segment-specific implementation beyond the insurer pack in HT-334.

## Acceptance Criteria

- [ ] The shared partner integration contract is documented and versioned.
- [ ] External identifiers avoid unnecessary policy, mortgage or purchaser PII.
- [ ] The contract supports aggregate reporting only by default.
- [ ] Vertical packs are expressed as configuration/content extensions, not schema forks.
- [ ] Insurer, mortgage-provider and new-build compatibility is assessed.
- [ ] Security and privacy review identifies any external dependency before implementation.
- [ ] A feature branch, PR and clean review loop are completed for any code change.

## Dependencies

- HT-328 scope gate accepted.
- HT-329, HT-331 and HT-332 architecture decisions.
