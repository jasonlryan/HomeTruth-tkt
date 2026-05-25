# HT-306: Wire canonical design tokens into frontend

**Priority:** P1
**Repo:** frontend
**Created:** 2026-05-25
**Updated:** 2026-05-25

## Goal

Make the frontend consume the canonical HomeTruth design-system tokens for
brand colours and typography, without attempting a full UI colour migration in
the same change.

## Description

The design-system baseline now defines canonical tokens in
`design-system/tokens/`. The frontend currently defines independent Tailwind
colour and font values, including off-brand blues and legacy font utilities.

This ticket creates the implementation bridge: frontend Tailwind should expose
HomeTruth token names and global CSS should define/import matching CSS custom
properties. Existing legacy Tailwind aliases may remain temporarily as
compatibility aliases, but they should point at canonical token values where
possible and be marked for later removal.

This ticket does not migrate every hardcoded JSX colour. That larger migration
belongs in a follow-up ticket after the token bridge exists.

## Files

- `HT_Frontend-staging/tailwind.config.js` — add `font-brand`, `font-chat`, and `ht.*` colour namespace
- `HT_Frontend-staging/src/index.css` — expose HomeTruth CSS custom properties and default font stacks
- `HT_Frontend-staging/src/...` — replace existing `font-gill` usages with `font-brand`
- `HomeTruth-tickets/open/HT-306-wire-design-tokens-into-frontend.md` — implementation log

## Acceptance Criteria

- [x] Frontend Tailwind exposes `font-brand` and `font-chat`.
- [x] Frontend Tailwind exposes an `ht.*` colour namespace aligned with `design-system/tokens/tokens.css`.
- [x] Existing legacy colour aliases either remain mapped to canonical tokens or are removed only when no usages remain.
- [x] Existing `font-gill` usages are migrated to `font-brand`.
- [x] Chat/system-font surfaces continue to have a system font utility.
- [x] Build or equivalent verification runs successfully, or the ticket records why it could not be run.
- [x] Implementation log records the files changed, verification, and follow-up migration risks.

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: added `font-brand`, `font-chat`, and `ht.*` design-token namespaces
  to `tailwind.config.js`; mirrored the canonical design-system CSS variables in
  `src/index.css`; mapped legacy colour aliases to canonical token values where
  possible; migrated existing `font-gill` usages to `font-brand`; changed the
  document chat wrapper from `font-inter` to `font-chat`.
- Verification: `npm run build` completed successfully. Build reported existing
  ESLint warnings for unused values in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`; those warnings were not introduced by this ticket.
- Notes: this creates the token bridge only. Many JSX files still contain
  hardcoded colour values and legacy utility names; those should be migrated in
  a follow-up ticket after visual review.
