# HT-345: Homeowner demo workspace for 19 November

**Status:** Complete
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
- Final user authorisation: review repeatedly, align styling, merge frontend PR #10, pull main, rehearse homeowner and Operations on main, and leave the local demo running.

## Final verification — 18 November 2026
- Frontend PR https://github.com/jasonlryan/HomeTruth-fe/pull/10 merged at 15:50 UTC; main 8b791be2b020a185d273ff7bb49eaa21b1187164. Backend main 0e0969035eb4c8afae1f2a014ea3d605038f7fb0.
- Repeated clean-main diff/caller review, with fixes on feature/ht-345-homeowner-demo-workspace only. Final reviewed feature head a3b57513561ebdbecfff3b583425b9741422c289.
- Fixed source preview contract, focus handling, independent authorised deep-link lookup, shared brand colours and contrast, page-title alignment, keyboard sidebar controls, and responsive cards/workspace. No remaining actionable findings in reviewed scope.
- Merged main: full CI=true test command passes 8 suites / 26 tests with no exclusions; CI=true production build succeeds. Removed obsolete starter test, added relevant deep-link/sidebar tests, removed unreachable unused handlers that blocked lint.
- Fresh browser rehearsal on merged main: sign-in, home history, all three source links, survey Preview/Chat and fresh source-limited answer, quote/invoice deep links and refresh selection, fresh property comparison, save answer, compact note/full View and persistence after reload.
- Comparison retains proposed versus recorded work, GBP 360, payment unknown, internal damp unassessed and staining cause unestablished.
- Operations on merged main: Overview; Home records search/view/links; Knowledge review; Programmes review and invitation preview; Connections choice/save; Content review. Desktop and 390px layouts visually inspected.
- Local frontend supervised from HT_Frontend-staging main at http://localhost:3000/property-profile; Operations http://localhost:3000/operations; December reference remains port 3001. API 8005 and Qdrant 6333 listening. Sleep inhibitor active for tomorrow; keep Mac powered, plugged in and lid open.
- Inventory: /Users/jasonryan/Developer/HomeTruth/.local-runtime/investor-demo/target-inventory.txt. Screenshots: /Users/jasonryan/Developer/HomeTruth/output/playwright/ht345-*.
- Existing admin role boundaries preserved. No production deployment or external outreach. Product UI uses natural labels; private inventory records fixture and integration limits.

## Follow-up: direct local entry
Status: complete. User requests opening demo without entering credentials.
Scope: localhost-only opt-in /demo entry using normal backend authentication
for the synthetic Maya account; homeowner/Operations destinations; visible
entry links on local landing and login screens. No admin bypass, production
auth changes or embedded real-account credentials. Verify disabled gate,
authentication errors, fresh browser entry and full tests/build before PR review.

Direct entry follow-up: PR https://github.com/jasonlryan/HomeTruth-fe/pull/11 merged; main e7a6ed5. 30 tests pass, strict CI build passes. Reviewed diff and surrounding auth/routes from main; no remaining actionable findings. Edits only on feature/ht-345-direct-demo-entry. Fresh-session homeowner and Operations entry verified; main local service restored. Links /demo and /demo?to=operations, plus local landing/login buttons. No credential entry needed.

## Follow-up: responsive navigation and icon alignment
Status: complete. Scope: persistent collapsible left navigation, official
HT logo mark, distinct consistent navigation icons and accessible labels.
Collapsed rail at narrow widths; expand/collapse at desktop; all settings
routes remain available. No whole-site icon migration in this change.
Acceptance: navigation never disappears, active page readable, keyboard and
mobile navigation verified, token styling, tests/build and PR review pass.

Responsive navigation PR https://github.com/jasonlryan/HomeTruth-fe/pull/12 merged; main 976f33a. Final head 679248b. Full 33 tests and strict CI build pass; GitGuardian passed. Repeated diff/caller review from main fixed drawer focus traversal and backdrop focus restoration; no remaining actionable findings. Browser inspected at 390px/1440px and 800px on merged main. Official HT mark/lockup from design-system assets; one consistent 24px outline navigation family. Persistent rail, mobile drawer, labels, active state, Settings, Escape and keyboard behaviour verified. Main service left supervised on port 3000. Whole-site icons remain a mix of Lucide/Material Symbols/HT motifs; no complete global icon migration claimed.
