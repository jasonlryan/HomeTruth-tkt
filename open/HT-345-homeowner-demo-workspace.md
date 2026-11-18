# HT-345: Homeowner demo workspace for 19 November

**Status:** In progress
**Priority:** P0
**Repo:** HomeTruth-fe

## Objective
Bring December demo home history, combined document Preview/Chat and compact notes into main product UI and rehearse the fictional homeowner demo.

## Scope and workstreams
1. Property Profile history: labelled synthetic Maya / 18 Alder Walk fixture, dates, observation/quotation/contractor record, authorised document links, invoiced amount distinct from payment.
2. One accessible Preview/Chat workspace using existing authenticated APIs and persisted chat history.
3. Compact title/excerpt/date note cards with full detail, real persistence and editing.
4. Full target inventory including admin, legacy references, URLs, login and live/mock boundaries.

## Out of scope
History ingestion/migrations, payment verification, production deployment, external outreach, individual partner sharing, blockchain proofs and admin data in homeowner views.

## Acceptance criteria
- Synthetic history is visibly labelled, explicitly enabled and isolated to fictional demo account/home. No invented history on other homes.
- Survey is not a damp diagnosis; invoice is not payment proof; links use authorised linked documents.
- Preview/Chat retains selection and history, closes with Escape and restores focus.
- Bounded note excerpts; View shows full content; persistence/editing/budget compatibility retained.
- Desktop/mobile and full demo rehearsal on feature head; base-main PR review and appropriate checks pass.
- Full inventory with URLs, credentials, story/click path, homeowner/admin sections, live/mock limits and run instructions.

## User scope updates
- Full product/operator scope is required for tomorrow. Add an Operations presentation workspace (overview, home records, knowledge, programmes, connections, content) using local synthetic fixtures only, with no real admin API calls or role elevation.
- Do not differentiate Mock and Vision in user-facing labels; use natural product language. Presenter inventory records implementation boundaries privately. This overrides the initial explicit fixture-badge criterion.
- Local gate: focused/utility suites 22 tests pass. Full-suite obsolete App.test.js fails resolving react-router-dom on both clean main and feature; it still expects the removed Learn React boilerplate. Two existing unused-variable lint warnings cause CI=true build failure; normal production build succeeds. No unrelated lint/test cleanup introduced.

## Final verification — 18 November 2026
- Frontend PR: https://github.com/jasonlryan/HomeTruth-fe/pull/10
- Base: 707e18fbf67f3ea68209820bf4a8622c77494b34; head: 75a491f203af82e67c9c2680d17dd418dddc7827.
- Feature root HT_Frontend-ht335; clean base review root HT_Frontend-review-main. All code changes and review fixes stayed on feature/ht-345-homeowner-demo-workspace.
- Full diff/callers reviewed from main. Fixed nested interactive controls, focus traversal through hidden/inactive controls, JSON-vs-binary preview contract, and selection URL/refresh behaviour. No remaining actionable findings in changed scope.
- 6 suites / 23 tests pass (all feature and existing utility suites). Old App.test.js failure independently reproduced on clean main; normal production build passes with two unchanged unused-variable warnings. CI=true build treats those baseline warnings as errors; not claimed as a pass.
- Browser: authenticated home/history/source links; survey text preview; new document Q&A response with source limits; Preview/Chat retention; Escape/close; quotation and invoice deep-links; invoice URL retained after refresh.
- Browser: property-context quote/invoice answer retains proposed versus recorded work, £360 amount, payment unknown and internal assessment unknown. New answer saved; compact card > full View > refresh persist verified.
- Browser Operations: overview, search/filter/view records, knowledge review, programme name/review/invitation, preference save, content panels. Desktop and 390px screenshots inspected; no Mock/Vision badges added.
- Presentation fixture scope: opt-in local env flag, synthetic Maya account and exact fictional home for history. Operations makes no real admin API calls and changes no roles. Actual admin routes remain protected.
- Inventory: workspace .local-runtime/investor-demo/target-inventory.txt. Screenshots: output/playwright/ht345-*.
- Local frontend port 3000 is supervised on this feature head; API main 0e09690; December reference port 3001 unchanged. No production deployment or merge performed.
