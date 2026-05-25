# HT-007: Define ht-* colour palette in tailwind config

**Priority:** P1
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Add a proper `ht.*` colour namespace in `tailwind.config.js`. Remove off-brand
colours that do not appear in the canonical design-system palette.

## Files

- `tailwind.config.js` — lines 14-31

## Acceptance Criteria

- [x] Tailwind config has the canonical `ht.*` namespace for brand, accent and
  neutral colours.
- [x] Off-brand historical aliases are removed: `primary`, `myblue`,
  `softBlue`, `blurpleLight`, `customBlue`, `customActiveText`,
  `customActiveBlue`.
- [x] Tailwind colours are backed by CSS variables from the design-system token
  bridge.

## Notes

Earlier notes suggested retaining some legacy UI-chrome aliases. HT-306 and
HT-008 superseded that approach: canonical `ht.*` values now sit on top of CSS
custom properties, while neutral Tailwind utilities remain available through
Tailwind's default palette.

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: resolved by HT-306/HT-008. `tailwind.config.js` now exposes
  canonical `ht.*` colour entries backed by `src/index.css` variables, and the
  old off-brand aliases have been removed.
- Verification: `rg "primary|myblue|softBlue|blurpleLight|customBlue|customActive" src tailwind.config.js`
  only finds semantic CSS variable names such as `--color-action-primary`, not
  legacy Tailwind aliases.
