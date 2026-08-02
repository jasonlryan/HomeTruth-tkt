# HT-322: Close 500-user cohort launch gaps

**Priority:** P1
**Repo:** backend / frontend / docs / tickets
**Milestone:** 500-user insurer pilot readiness
**Created:** 2026-05-31
**Updated:** 2026-05-31

## Goal

Turn the 500-user partner cohort path from technically implemented into launchable, supportable and understandable for real users.

## Description

HomeTruth now has the core pilot mechanics:

- partner/cohort/consent model
- invite-led partner onboarding
- property profile setup
- document-to-property linking
- prevention tasks
- pilot analytics and aggregate reporting
- property-aware unified retrieval

The remaining risk is not one missing feature. It is that a cohort of 500 people needs a coherent introduction, a guided first session, an operational support path, clear deletion/withdrawal handling, and a measured go/no-go launch process.

This ticket coordinates the gap closure work and should be treated as the execution plan that feeds HT-318, HT-319 and HT-320.

## Dependencies

- HT-315: insurer invite and co-branded onboarding
- HT-316: prevention tasks and reminders
- HT-317: pilot analytics, reporting and readiness review
- HT-318: pilot support and incident runbook
- HT-319: data deletion and consent withdrawal runbook
- HT-320: production cohort setup and go/no-go review
- HT-321: property-aware unified retrieval layer
- HT-324: pilot reporting coverage and privacy validation

## Workstreams

### 1. Pilot Introduction And User Promise

**Goal:** Make every invited user understand why they have been invited, what HomeTruth will help them do in the first session, what data is and is not shared with the partner, and where to get help.

Define the exact way the insurer introduces users to HomeTruth.

Required outputs:

- partner invitation copy for email/app/landing route
- HomeTruth landing/onboarding copy for the pilot cohort
- plain-English user promise focused on homeowner value, not insurer compliance
- expected time commitment for first setup
- incentive or participation framing, if any
- support contact route included in pilot communications

User-facing value proposition:

- Build a useful home record in one place.
- Know which home documents matter and when they expire.
- Ask questions about your own property and uploaded documents.
- Get practical maintenance and prevention actions.
- Make future admin, maintenance, claims, selling or remortgaging less painful.

Acceptance criteria:

- [x] Partner invitation copy exists for email/app/landing route.
- [x] HomeTruth-hosted landing/onboarding copy exists for the pilot cohort.
- [x] Copy is homeowner-value-first and does not frame HomeTruth as insurer compliance.
- [x] Copy states expected setup time and first-session actions.
- [x] Copy explains aggregate reporting versus individual data sharing in plain English.
- [ ] Copy includes support contact route and response expectation.
- [ ] Incentive or no-incentive decision is recorded.
- [ ] Copy is reviewed by product and partner/compliance owner before launch.

### 2. First-Session Guided Journey

**Goal:** Move a new cohort user from invite to first useful HomeTruth outcome in one session: property record created, evidence added, actions generated and one property-aware answer received.

Make the first session concrete enough that users reach value quickly.

Target guided path:

1. Validate invite.
2. Sign up or log in.
3. Review and grant required consent.
4. Add or confirm property address, property type, tenure and relationship.
5. Upload or link two to three useful documents.
6. Generate property actions.
7. Ask one property-aware assistant question.
8. See a clear “what HomeTruth found” summary and next action list.

Recommended first-session document prompts:

- insurance policy
- EPC
- survey
- boiler or service certificate
- warranty or maintenance record
- evidence for a known issue

Acceptance criteria:

- [x] First-session flow is documented as screens, user actions and system responses.
- [x] Required fields for property setup are listed.
- [x] Recommended document prompts are shown in the journey.
- [x] Empty, skipped and failed document-upload states are defined.
- [x] Task-generation step is included and explains what the user should do next.
- [x] Property-aware assistant prompt examples are included.
- [x] “What HomeTruth found” summary content is defined.
- [x] Drop-off points are mapped to pilot analytics events.

### 3. Property-Aware Chat Integration

**Goal:** Ensure the assistant uses the selected property context when a user asks from the property journey, while keeping all-document behaviour explicit outside property context.

Confirm the frontend sends selected property context to the authenticated assistant.

Required outputs:

- chat UI has a clear selected-property context when launched from a property profile
- authenticated chat request includes `propertyId` or `property_id` when a property is selected
- fallback behaviour is clear when no property is selected
- source-class behaviour is smoke-tested for uploaded document, property record and HomeTruth guidance context

Acceptance criteria:

- [x] Frontend `askAIChat` can pass `propertyId` to `/api/ai_chat/chat`.
- [x] Property profile has a clear “Ask about this property” entry point or equivalent.
- [x] Selected property context survives navigation into the chat surface.
- [x] Request payload includes `propertyId` when launched from a selected property.
- [x] No selected property falls back to all current-user documents by explicit product decision.
- [ ] Browser/API smoke test verifies property-scoped context metadata in the chat response.
- [x] A follow-up implementation ticket exists if any of the above is not already true.

### 4. Support And Incident Readiness

**Goal:** Make support ownership and escalation explicit enough that a confused user, failed invite, data concern or technical incident has a known route and response expectation during the pilot.

Close HT-318 with named human owners and response expectations.

Required outputs:

- named pilot support owner
- named technical escalation contact
- named incident owner
- support hours and first-response target
- issue categories: invite failure, signup/login, consent question, property setup, document/task issue, data deletion/withdrawal, incident
- severity levels and escalation rules
- user-facing holding replies for common support cases
- incident communication path
- admin monitoring route reference

Acceptance criteria:

- [ ] Pilot support owner is named.
- [ ] Technical escalation contact is named.
- [ ] Incident owner is named.
- [ ] Support hours and first-response target are recorded.
- [x] Issue categories are defined.
- [x] Severity levels and escalation rules are defined.
- [x] User-facing holding replies are drafted.
- [x] Incident communication path is documented.
- [x] Admin monitoring/reporting route is referenced.
- [x] HT-318 is completed or explicitly blocked with named missing inputs.

### 5. Consent Withdrawal And Deletion Readiness

**Goal:** Define what happens when a user withdraws consent or requests deletion, including MySQL, Qdrant, pilot events and partner-reporting implications.

Close HT-319 before any live pilot launch.

Required outputs:

- withdrawal behaviour for each consent scope:
  - `hometruth_processing`
  - `partner_reporting`
  - `aggregate_analytics`
  - `individual_report_access`
  - `partner_contact_servicing`
- deletion/anonymisation mapping for users, cohort members, consent records, properties, documents, facts, tasks, Qdrant chunks and pilot events
- process states: requested, verified, in progress, completed, rejected, escalated
- identity verification requirement
- target handling time and escalation rule
- partner reporting implication when consent is withdrawn
- manual DB/admin steps or a follow-up tooling ticket
- legal/privacy review sign-off requirement

Acceptance criteria:

- [x] Withdrawal behaviour is defined for every consent scope.
- [x] Delete versus anonymise decision is mapped for every major data object.
- [x] Qdrant chunk deletion/backfill implications are documented.
- [x] Request process states are defined.
- [x] Identity verification requirement is documented.
- [ ] Target handling time and escalation rule are recorded.
- [x] Partner-reporting impact is documented.
- [x] Manual DB/admin steps are listed or a follow-up tooling ticket is created.
- [ ] Legal/privacy review owner and status are recorded.
- [x] HT-319 is completed or explicitly blocked with named missing inputs.

### 6. Operational Scale And Reliability Check

**Goal:** Prove the pilot can run for 500 users on the target environment without discovering basic migration, Qdrant, upload, retrieval or reporting failures after launch.

Prove the path is viable for 500 users before launch.

Required outputs:

- target environment confirmed
- migration status recorded for target backend
- Qdrant collections confirmed for `home_truth_documents` and `user_documents`
- upload/document processing smoke-tested with realistic file sizes
- property-aware assistant smoke-tested against real MySQL/Qdrant/OpenAI
- known upload latency or retry risks recorded
- decision on whether synchronous embedding is acceptable for V1 pilot or needs queueing before launch

Acceptance criteria:

- [ ] Target environment is named.
- [ ] Backend migration status is recorded from the target environment.
- [ ] Qdrant collections and vector dimensions are confirmed.
- [ ] Realistic document upload/link smoke test is completed.
- [ ] Property-aware chat smoke test is completed against real services.
- [ ] Admin aggregate report smoke test is completed.
- [ ] Upload and embedding latency are recorded.
- [ ] Retry/failure behaviour for document processing is reviewed.
- [ ] Queueing decision for V1 pilot is recorded.

### 7. Pilot Measurement And Success Thresholds

**Goal:** Define measurable success before launch so the 500-person pilot produces evidence instead of just usage counts.

Define what success looks like before the cohort starts.

Required outputs:

- activation target
- property setup completion target
- average documents linked per active user target
- task generation and completion targets
- repeat-use target
- user feedback score target
- drop-off thresholds requiring intervention
- partner-facing aggregate reporting pack outline

Suggested starting thresholds to review:

- 60% invite-to-signup activation
- 70% signup-to-property-complete rate
- 2+ documents linked per activated user
- 1+ generated action viewed per activated user
- 25% of activated users complete or dismiss at least one action
- 20% of activated users ask at least one property-aware assistant question
- average feedback rating of 4/5 or better

Acceptance criteria:

- [x] Activation, setup, document, task, chat, repeat-use and feedback targets are recorded.
- [x] Drop-off thresholds that trigger intervention are recorded.
- [x] Pilot event names are mapped to each metric.
- [x] Admin aggregate report can answer each metric or a follow-up reporting ticket is created.
- [x] Partner-facing aggregate reporting pack outline is drafted.
- [ ] Reporting pack is reviewed for privacy leakage by the privacy/compliance owner; HT-324 technical boundary checks are complete.
- [ ] Decision owner for success/no-success interpretation is named.

### 8. Final Go/No-Go

**Goal:** Make the launch decision explicit, evidence-backed and reversible, with all blockers and monitoring expectations recorded.

Close HT-320 only after the operational blockers are resolved.

Required outputs:

- production/staging target environment recorded
- partner and cohort records configured
- invite mode confirmed: cohort code, individual invite codes or both
- consent copy version recorded
- required and optional consent scopes reviewed
- end-to-end smoke test completed
- admin pilot report reviewed for aggregate-only output
- open risks and blockers listed
- final `go`, `go_with_monitoring` or `no_go` decision recorded with owner/date

Acceptance criteria:

- [ ] Production/staging target environment is recorded.
- [ ] Partner and cohort records are configured.
- [ ] Invite mode is confirmed.
- [ ] Consent copy version is recorded.
- [ ] Required and optional consent scopes are reviewed.
- [ ] End-to-end pilot smoke test is complete.
- [ ] Admin pilot report is reviewed for aggregate-only output.
- [x] HT-318 and HT-319 status is reflected in the launch decision.
- [x] Open risks and blockers are listed.
- [ ] Final decision is recorded as `go`, `go_with_monitoring` or `no_go` with owner/date.

## Acceptance Criteria

- [ ] Pilot invitation and onboarding copy are drafted and reviewed.
- [x] First-session user journey is documented as a step-by-step guided flow.
- [x] Frontend property-aware chat handoff is verified or a follow-up implementation ticket is created.
- [x] HT-318 support and incident runbook is completed or explicitly blocked with named missing inputs.
- [x] HT-319 deletion and consent withdrawal runbook is completed or explicitly blocked with named missing inputs.
- [ ] Target environment, migration state and Qdrant collection readiness are recorded.
- [ ] End-to-end pilot smoke test covers invite view, auth, consent, property setup, document upload/link, task generation, property-aware chat and aggregate admin report.
- [x] Pilot success thresholds are recorded before launch.
- [ ] Partner-facing aggregate report outline is drafted and awaits privacy/compliance review; HT-324 technical boundary checks are complete.
- [x] HT-320 go/no-go review is updated with the final decision or remaining blockers.
- [x] Implementation log records changed files, decisions and verification performed.

## Review / Decision Gate

This ticket should not be marked complete until HT-318, HT-319 and HT-320 are either completed or have explicit named blockers. The pilot should remain `no_go` until support ownership, deletion/withdrawal handling and target-environment smoke testing are accepted.

## Implementation Log

### 2026-05-31
- Repo: tickets
- Changed: created HT-322 as the 500-user cohort gap-closure execution plan.
- Verification: derived from current HT-314 through HT-321 implementation state and open HT-318, HT-319 and HT-320 blockers.
- Notes: this ticket coordinates launch readiness; implementation may require follow-up frontend/backend tickets where verification finds missing product behaviour.

### 2026-05-31
- Repo: docs, tickets
- Changed:
  - added per-workstream goals and acceptance criteria to HT-322
  - `hometruth DOCS/docs/product/500-user-cohort-launch-plan.md`
  - `hometruth DOCS/docs/product/pilot-support-incident-runbook.md`
  - `hometruth DOCS/docs/product/data-deletion-consent-withdrawal-runbook.md`
  - `hometruth DOCS/docs/product/pilot-go-no-go-review.md`
  - `HomeTruth-tickets/open/HT-318-pilot-support-incident-runbook.md`
  - `HomeTruth-tickets/open/HT-319-data-deletion-consent-withdrawal-runbook.md`
  - `HomeTruth-tickets/open/HT-320-production-cohort-setup-go-no-go.md`
  - `HomeTruth-tickets/open/HT-323-wire-property-aware-chat-frontend.md`
- Verification:
  - frontend inspection found property-aware backend support is not yet wired through `askAIChat` / property profile, so HT-323 was created
  - operational docs drafted for launch journey, support, deletion/withdrawal and go/no-go
- Notes:
  - loop status remains `no_go` because human owners, privacy/legal review, target environment and smoke test are still missing
  - next implementation move is HT-323 plus owner/legal/environment decisions for HT-318, HT-319 and HT-320

### 2026-05-31
- Repo: frontend, docs, tickets
- Changed:
  - implemented HT-323 frontend property-aware chat handoff
  - created HT-324 reporting coverage and aggregate privacy validation ticket
  - updated `hometruth DOCS/docs/product/500-user-cohort-launch-plan.md` with pilot event mapping
  - updated `hometruth DOCS/docs/product/pilot-go-no-go-review.md` to reflect frontend implementation and remaining smoke-test blocker
  - updated HT-322 and HT-323 acceptance criteria status
  - `HomeTruth-tickets/open/HT-324-validate-pilot-reporting-coverage-and-privacy.md`
- Verification:
  - `npm run build` passes in `HT_Frontend-staging`
  - build still reports pre-existing unrelated lint warnings in `KnowledgeBaseAdmin.jsx` and `DataPrivacySettings.jsx`
- Notes:
  - loop status remains `no_go`
  - remaining blockers are human owner assignment, support route/response target, privacy/legal acceptance, target environment readiness, real service smoke tests and privacy review of the aggregate report pack

### 2026-08-02
- Repo: backend, docs, tickets
- Changed: HT-324 now measures activation, setup, documents, task engagement, property-aware chat and feedback as aggregate cohort metrics; repeat use is explicitly `not_instrumented`.
- Verification: representative five-member MySQL cohort-report smoke passed with full fixture cleanup and response-boundary assertions.
- Notes: HT-326 is the concrete next feature needed to make repeat use reportable. Partner-facing privacy/compliance approval remains a human launch blocker.

### 2026-08-02
- Repo: backend, frontend, docs, tickets
- Changed: HT-326 implements consent-bound daily activity and the aggregate repeat-use metric; the reporting response now marks repeat use as measured.
- Verification: two-member MySQL smoke passed with same-day dedupe, two-day repeat counting and full fixture cleanup.
- Notes: code is awaiting review in backend PR #4 and frontend PR #2. The pilot remains `no_go` pending target-environment, owner and privacy/compliance decisions.
