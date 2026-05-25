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

- [ ] Frontend Tailwind exposes `font-brand` and `font-chat`.
- [ ] Frontend Tailwind exposes an `ht.*` colour namespace aligned with `design-system/tokens/tokens.css`.
- [ ] Existing legacy colour aliases either remain mapped to canonical tokens or are removed only when no usages remain.
- [ ] Existing `font-gill` usages are migrated to `font-brand`.
- [ ] Chat/system-font surfaces continue to have a system font utility.
- [ ] Build or equivalent verification runs successfully, or the ticket records why it could not be run.
- [ ] Implementation log records the files changed, verification, and follow-up migration risks.

## Implementation Log
