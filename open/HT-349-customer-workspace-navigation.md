# HT-349 · Customer workspace and navigation upgrades

**Status:** Open · first implementation on `feature/ht-348-homepage-components`
**Related:** HT-348 (shared homepage journey), HT-340 (intent-based onboarding), HT-345 (homeowner demo workspace)

## Objective

Help customers go from a question or task to a useful, evidence-linked home record. Make it clear which home they are working on, what needs attention and how to resume their work.

## Scope and order

- [x] **First slice — public entry and signed-in navigation.** Label the homepage link **About HomeTruth** and lead to the existing How it works content. Put **Ask HomeTruth** in the signed-in top bar. Use **Vault**, **Notebooks**, and **Tools** in customer navigation, with the existing Budget Calculator listed under Tools. Preserve existing routes and Settings. Use HomeTruth icons and shared navigation states for the touched shell.
- [ ] **Version the three user flows.** Specify Buying (viewing checklist, survey evidence, follow-up, buyer-to-owner continuity), Improving (job scope, quote comparison, budget, invoice and warranty), and Selling (paperwork checklist, documented work, review and selective sharing). Specify first useful results, what is saved, return points, and the ontology and permissions at each step. Make help available from each task and preserve its context when signing in.
- [ ] **Design the Control centre.** Reuse the existing Property profile, work history, facts and next actions. Let people resume their current task before setup and see what needs attention for a selected home after setup. Keep property details inside the home record. Validate a survey finding → source passage → follow-up → home record journey first.
- [ ] **Design multiple-property context.** Define how to add and switch homes, confirm the relationship per property, and apply the selection to Vault, Notebooks, Tools and Ask HomeTruth. A buyer and owner relationship can coexist for different properties. Verify cross-property and cross-user isolation before shipping.
- [ ] **Rework Admin navigation.** Use the clear Admin grouping from the port 3001 reference. Give Knowledge ingestion and source review, Reporting, Partner programmes, Content, Product resources and sensitive Data access explicit destinations. Keep the shared sign-in. Verify permissions for each destination, including direct URLs and exports. The demo Data Room uses fabricated records.
- [ ] **Apply the design system through real flows.** Start with the signed-in shell, then Home record → Vault → evidence → next action. Use the current typography, HT icons, first-line alignment and shared hover, selected, focus, inactive, loading, empty and error states. Extend that reference to Notebooks, Tools, Settings and Admin.

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
