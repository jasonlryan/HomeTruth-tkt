# HT-356 · Find the right appliance manual from Ask or the homepage

**Repo:** both
**Priority:** P1
**Created:** 2026-11-19
**Status:** Open

## Homeowner outcome

“Can you find the manual for my washing machine?” is one job. The homeowner should be able to ask it without knowing which documents HomeTruth holds. Show the right saved manual when possible, explain what is known about its edition, and help find and keep the official copy when needed. Let the homeowner ask a question and see the passage that supports the answer.

## Entry and action contract

- Typed Ask offers a selectable **Find a manufacturer’s manual** action for a manual-finding request. The action payload is `{ "actionId": "find_appliance_manual" }`. Both the anonymous and signed-in Ask clients should understand this offer. Keep ordinary questions conversational, including questions about the contents of a manual already selected.
- Reuse the same action ID already carried by the Improving starter in HT-349 / frontend PR #16. Route by ID so changing the label or language preserves behaviour. Public entry opens the labelled preview and can carry the intent through sign-in. Selecting the starter, submitting a question, navigating, resuming after login and refreshing each make zero paid specialist calls.
- In the live signed-in pilot, open the selected home’s appliance picker or reuse the appliance context. Resolve ambiguous appliances with the homeowner. Use the HT-341 identification flow if the full model is missing. The server rechecks property, item and document access at use time. A remembered action carries intent only.
- Keep selection of a known action in the product handoff layer. The backend maps it to the existing appliance endpoint, registry and domain service. The client cannot choose a runtime revision, tool or spending limit. Parent/child messaging is outside this ticket.

## Manual resolution and acceptance

1. **Do we have it?** Inspect the appliance’s private evidence and relevant authorised home documents. Offer an existing exact-model manual with its source and a way to open it or ask a question. If an unlinked document is a possible match, show the evidence for that match and ask before associating it. Handle multiple variants, unreadable files and unavailable sources explicitly. A user with read access may open permitted evidence; lookup and import require their existing write permissions.
2. **Is it current?** Show the exact model/variant and market, edition or revision, source, and last verification date where known. An exact match can still have unknown currency. Say “latest edition unverified” when the manufacturer provides insufficient evidence. A recent upload or successful indexing does not establish currency. If a newer official edition is evidenced, show both and offer review. Keep the existing copy and its provenance until the homeowner acts.
3. **Find it if needed.** When the manual is missing, mismatched, superseded or the homeowner wants to check for an update, identify the selected home, appliance and complete model on an explicit **Confirm appliance and search** control. Only this action can start a paid manufacturer lookup. Use the existing item-scoped manual-search POST and a stable request key for retries. An external currency check that incurs a paid lookup uses the same gate. Respect pilot availability and HT-351 admission. Offer an official finder or upload when a lookup cannot run or finds no verified match.
4. **Keep it and answer from it.** Show cited candidates. The homeowner separately confirms which candidate to save. Reuse HT-341’s verified PDF import, deduplication, private appliance association, provenance and indexing. Show pending, ready or failed indexing accurately. Retrying indexing must reuse the saved document. A support-page link alone cannot support a claim about the manual’s contents. Once ready, answer from authorised evidence with a verifiable passage citation; surface an unknown when evidence is missing.
5. **Is there a warranty?** Offer an optional warranty check from the result without interrupting the manual journey. Reuse HT-341 purchase and warranty evidence. Show sourced terms, relevant dates and uncertainties; distinguish a manufacturer's general warranty from evidence of this unit's purchase, registration or coverage. If unresolved, offer to attach a receipt or warranty document. Warranty lookup never silently starts another paid manual search.

## Verification before closure

- Exercise the public starter, anonymous typed Ask, sign-in continuation and authenticated typed Ask. Each resolves the same action ID. Verify the preview with pilot off and the live picker with pilot on. Include unrelated prompts and an already-selected manual question.
- Count specialist calls and reservations. Existing saved manual, ambiguous item, preview, cancellation, navigation and refresh produce zero. Explicit confirmation and a duplicate submission produce one paid run. Permission loss or cross-home scope prevents disclosure and execution.
- Use fixtures for an exact current edition, unknown edition, a superseded edition, a different model suffix, and no match. Verify separate search and save confirmations, preserved history, deduplication, indexing failure/retry, a passage-backed answer after reload, and warranty evidence present/absent.

**Delivery dependencies:** HT-349 chooser, HT-341 appliance record/import, HT-350 dispatcher and HT-351 admission. Coordinate pilot release evidence with HT-354. Issue-specific videos are a separate enhancement in [HT-357](HT-357-appliance-troubleshooting-videos.md).
