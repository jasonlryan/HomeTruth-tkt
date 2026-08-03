# HT-328: Build the reusable B2B partnership foundation

**Priority:** P1
**Repo:** backend / frontend / docs / tickets
**Milestone:** B2B2C partner-programme foundation
**Created:** 2026-08-02
**Updated:** 2026-08-03

## Goal

Deliver the functional B2B partnership foundation that lets HomeTruth run partner programmes for insurers, mortgage providers, home developers and other B2B clients without a bespoke product fork per client.

## Objective

Build a shared partner-programme core around the existing partner, cohort and consent foundation. It must support programme configuration, branded acquisition, governed partner roles and aggregate evidence while preserving homeowner ownership and explicit-consent boundaries.

## Scope

- Generic partner types, including insurer, mortgage provider, home developer and other B2B client.
- A reusable programme lifecycle: partner, programme, cohort, campaign, entitlement, invite route, status and closure.
- Partner-aware, co-branded acquisition and onboarding that retains the HomeTruth homeowner promise.
- Separate processing, analytics, partner-reporting and partner-contact consent choices.
- Governed partner roles with aggregate-only reporting by default, audit evidence and explicit denials for individual homeowner data.
- Configurable vertical packs for content, document prompts, task rules and measures, starting with an insurer reference pack.

## Out Of Scope

- An insurer-only architecture or schema fork.
- A bespoke application for each mortgage provider, home developer or other client.
- Default individual-data sharing, partner task control or partner property control.
- Claims, underwriting, pricing, credit, valuation or regulated-advice decisions.
- SSO, CRM integrations or external APIs before a committed requirement validates them.

## Functional Workstreams

1. **Programme administration, HT-329:** operator-configured partner, programme, cohort, campaign and lifecycle management.
2. **Partner acquisition, HT-330:** programme-aware invitation, co-branding, attribution and consent journey.
3. **Governed access, HT-332:** partner roles, programme-scoped authorization and audit controls.
4. **Programme evidence, HT-331:** thresholded aggregate partner dashboard and decision-ready reporting.
5. **Integration and configuration contract, HT-333:** stable identifiers, handoff patterns and vertical-pack configuration.
6. **Insurer reference pack, HT-334:** reusable policy/prevention content and measures built on the common core.

## Acceptance Criteria

- [x] Functional B2B partnership direction is defined for insurers, mortgage providers, home developers and other B2B clients.
- [x] The shared core and vertical-pack boundary are documented.
- [x] Functional workstreams are ticketed and sequenced.
- [x] A partner programme can be configured, activated, paused and closed without a code change for each client.
- [ ] An invited homeowner receives the correct programme context and can make separate consent choices.
- [ ] Partner roles are programme-scoped, auditable and denied individual homeowner data by default.
- [ ] A partner can view decision-ready, thresholded aggregate programme evidence only.
- [ ] The insurer reference pack runs on the shared core without an insurer-specific fork.
- [ ] Mortgage-provider and home-developer requirements can be expressed as configuration or vertical-pack extensions without changing the shared access model.
- [ ] Each implementation workstream has completed the feature-branch PR review/fix loop and is merged.

## Dependencies

- HT-314: partner cohort and consent foundation
- HT-315: invite-led partner onboarding
- HT-317, HT-324 and HT-326: pilot reporting and repeat-use foundations
- HT-320: current live-cohort go/no-go remains independent and must not be bypassed

## Implementation Log

### 2026-08-02
- Repo: docs, tickets
- Changed: reframed HT-328 as the active functional B2B partnership foundation, with generic partner-programme capabilities delivered through HT-329 through HT-334.
- Verification: direction supplied directly by the product owner: support insurers, mortgage providers, home developers and other B2B clients through a shared core.
- Notes: insurers are a reference pack, not a product fork. Code implementation is outstanding.

### 2026-08-03
- Repo: backend, frontend, tickets
- Changed: completed and merged HT-329, providing shared operator-controlled partner, programme, campaign, cohort and lifecycle administration for insurer, mortgage-provider, home-developer and other B2B client types.
- Verification: backend PR #5 merged as `06efd28c8acab65a882d6877063c935c2f573d85`; frontend PR #3 merged as `86c9338429a37ccf5b45bf1fe2d507c8d689227f`; both clean `main` worktrees were fast-forwarded and verified against `origin/main`.
- Notes: HT-328 remains open. HT-330 is the next planned functional workstream and must build programme-aware acquisition and consent on the shared HT-329 lifecycle rather than introducing a vertical-specific path.
