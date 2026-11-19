# HT-349 · Customer workspace and navigation upgrades

**Status:** Open · initial frontend rollout merged in PR #13
**Related:** HT-348 (shared homepage journey), HT-340 (intent-based onboarding), HT-345 (homeowner demo workspace)

## Objective

Help customers go from a question or task to a useful, evidence-linked home record. Make it clear which home they are working on, what needs attention and how to resume their work.

## Scope and order

- [x] **First slice — public entry and signed-in navigation.** Label the homepage link **About HomeTruth** and lead to the existing How it works content. Put **Ask HomeTruth** in the signed-in top bar. Use **Vault**, **Notebooks**, and **Tools** in customer navigation, with the existing Budget Calculator listed under Tools. Preserve existing routes and Settings. Use HomeTruth icons and shared navigation states for the touched shell.
- [x] **Version the three user flows.** Specify Buying (viewing checklist, survey evidence, follow-up, buyer-to-owner continuity), Improving (job scope, quote comparison, budget, invoice and warranty), and Selling (paperwork checklist, documented work, review and selective sharing). Specify first useful results, what is saved, return points, and the ontology and permissions at each step. Make help available from each task and preserve its context when signing in.
- [ ] **Design the Control centre.** Reuse the existing Property profile, work history, facts and next actions. Let people resume their current task before setup and see what needs attention for a selected home after setup. Keep property details inside the home record. Validate a survey finding → source passage → follow-up → home record journey first.
- [ ] **Design multiple-property context.** Define how to add and switch homes, confirm the relationship per property, and apply the selection to Vault, Notebooks, Tools and Ask HomeTruth. A buyer and owner relationship can coexist for different properties. Verify cross-property and cross-user isolation before shipping.
- [x] **Rework Admin navigation.** Use the clear Admin grouping from the port 3001 reference. Give Knowledge ingestion and source review, Reporting, Partner programmes, Content, Product resources and sensitive Data access explicit destinations. Keep the shared sign-in. Verify permissions for each destination, including direct URLs and exports. The demo Data Room uses fabricated records.
- [x] **Apply the design system through real flows.** Start with the signed-in shell, then Home record → Vault → evidence → next action. Use the current typography, HT icons, first-line alignment and shared hover, selected, focus, inactive, loading, empty and error states. Extend that reference to Notebooks, Tools, Settings and Admin.

## Boundaries

The first slice uses existing capabilities and preserves compatibility. New project notebooks, quote comparison, sale-pack sharing and multi-property features need their own flow and data decisions. No production rollout, valuation claims, or expansion of data-access privileges in the first slice.

## Acceptance and verification

- Browser-check signed-out and signed-in homepage entry, linked legacy information, customer and admin navigation, and deep links.
- Check narrow and wide layouts plus keyboard focus, selected state and mobile navigation. Run the frontend tests and production build.
- Review journey prototypes with the user before implementing their persistent data or permissions. Attach verification evidence and PR links to this ticket as each workstream lands. Keep the ticket open for the remaining work.

## 18 November 2026 — first slice available for localhost review

- Frontend commit `faadf4e` on `feature/ht-348-homepage-components`.
- Both homepage variants link **About HomeTruth** to `/how-it-works`. The signed-in top bar links to Ask HomeTruth. Vault and Notebooks use the existing document and saved-item URLs. Tools has a dedicated landing page and links to the existing calculator.
- The signed-in navigation uses the HT icon suite and the catalogue and Claude pack carry the updated shared homepage copy.
- Browser checks at 1440 and 390px covered the public links, Tools sign-in gate, navigation destinations and selected states, mobile drawer, icon assets and admin visibility. All 33 frontend tests and the strict production build passed. Existing Sidebar test fixtures emit React `act` warnings.
- Next workstream for review: version the three customer journeys and show the buying survey-to-follow-up sequence in the Control centre proposal. Feature code is local for review.

## 18 November 2026 — feature preview and conversation follow-up

- `3ec5642`: `npm run start:branch-preview` makes port 3012 open the question preview from its root. Buying, Improving and Selling keep their official 24px icons above the labels. Verified all three routes and icon alignment at 390, 760 and 1440px.
- `878a89b`: signed-in Ask HomeTruth reserves room for the opening at Send, moves the pane only if needed and leaves scroll under user control as the answer grows. **Jump to latest** is available above the composer when there is more to read. Browser checks covered first and follow-up questions, manual interruption, keyboard focus and reduced motion using local reply fixtures. All 33 frontend tests and the strict build passed.

## 18 November 2026 — official icons in the app

- `606e72b` replaces Lucide and Material Symbols UI glyphs and the remaining inline control icons with the HomeTruth design system. The app loads the same 166-symbol SVG sprite as the catalogue. Kept accessible names for icon-only controls and removed the external Material Symbols font request.
- Browser checks confirmed SVG geometry actually rendered in Property profile, Vault, the document workspace, Ask HomeTruth and Admin, including the mobile property screen and keyboard document close. All 33 tests and the strict build passed.
- The remaining design-system workstream covers page typography, layouts, component states and the complete evidence-to-next-action flow.

## 18 November 2026 — blueprints and Control centre review

- `08a1d5f` adds HT-FLOW-002 Buying, HT-FLOW-003 Improving and HT-FLOW-004 Selling, version 0.1. The localhost Admin UX specifications page exposes each with a stable URL and versioned download. Verified the links, downloads, direct navigation and mobile layout.
- `8ffa512` adds an event-led Control centre proposal at `http://localhost:3012/workspace-preview`. Upcoming shows a sample booked boiler service. Needs attention shows a sample stale connection and saved follow-ups. Surveys are reviewed in Vault. Manuals open from the appliance, and connection access is explained in the connection view.
- Browser-checked the survey → passage → editable follow-up → Control centre → passage round trip, the appliance and connection handoffs, mobile layout and the absence of API traffic. The proposal uses sample data and leaves the underlying records, permissions and connection setup for review.

## 18 November 2026 — draft PR

- [Frontend PR #13](https://github.com/jasonlryan/HomeTruth-fe/pull/13) tracks the homepage and signed-in work, including the design-system rollout. Head at opening was `8ffa512`, targeting `main`.
- Keep the PR in draft while the signed-in rollout and final review are in progress. Use a merge commit so individual job commits remain in history.

## 18 November 2026 — Admin workspace in PR #13

- `567fb1b` adds an Admin overview and shared menu with distinct destinations for Knowledge, Reporting, Partner programmes, Content, Product resources and Data access. Existing URLs use one protected route tree. Knowledge retains source ingestion, library and indexing controls.
- Browser checks covered all seven direct routes for signed-out visitors, customers and admins, the selected state, the mobile overview, a keyboard navigation action and a synthetic CSV download. The local backend returned HTTP 401 for an unsigned export request and 403 for the customer test account. The strict production build and all 33 tests passed.
- No new privileges were introduced. The broader design-system rollout remains in progress in draft PR #13.

## 19 November 2026 — frontend rollout merged

- [Frontend PR #13](https://github.com/jasonlryan/HomeTruth-fe/pull/13) merged as `aa063c7`, preserving the feature commits, and the local frontend main checkout is up to date.
- The signed-in workspace uses the shared typography, icons and component states. Vault supports keyboard upload and filters, and a customer can return from an evidence preview to the correct home record and its next actions. The first homepage answer remains available after sign-in and refresh. The Admin design reference and versioned blueprints are included in the build.
- All 37 frontend tests, the strict build from tracked files, GitGuardian and browser checks passed. The browser pass used local fixtures for the routes that require data and sign-in.
- HT-349 remains open for persistent Control centre workflows and multiple-home context.

## 19 November 2026 — selected-home Control centre

- Implement the signed-in overview on a separate feature branch. Read homes available through Property Person and group open Reminder / Task records into future dates, overdue items and undated follow-ups.
- Use existing property-task permissions and persistence. Customer-entered follow-ups and existing service or document date reminders are in scope. Calendar booking, recurring events, appliance connections and a site-wide home selector are follow-on work.
- Verify persistence, completion, retry, read and write permissions, home switching, source navigation and desktop and mobile layout.

- Local review is available at http://localhost:3013/control-centre. Drafts are [frontend #15](https://github.com/jasonlryan/HomeTruth-fe/pull/15) at `d80b088` and [backend #13](https://github.com/jasonlryan/HomeTruth-be/pull/13) at `0f50342`.
- Verified sign-in, signed-in navigation, real local MySQL save and completion across refresh, desktop and mobile layout, home switching, read-only permissions and denied cross-home access. Six groups of concurrent retries each produced one task and one status entry. All 38 frontend tests, the strict production build and existing backend tests passed.
- The upcoming section displays recorded reminder dates. Confirmed bookings and direct passage capture for new follow-ups are still open.
