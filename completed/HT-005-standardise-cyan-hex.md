# HT-005: Standardise cyan to single hex value

**Priority:** P2
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Three different cyan values were used: #00c0f9, #00bfff, and #19B0F0. This
ticket originally proposed standardising all to #00c0f9, but that proposal has
been superseded by the canonical HomeTruth design-system token `--ht-cyan:
#00B4D8`.

## Files

- `src/components/Navbar.jsx` — 4 instances of #00bfff
- `src/index.css` — #19B0F0 in bullet SVG
- `src/components/AttitudinalQuizModal.jsx` — #19B0F0F0
- `tailwind.config.js` — customActive/customActiveText/customActiveBlue all use #19B0F0 variants

## Acceptance Criteria

- [x] Cyan brand usage is centralised through canonical `ht.*` tokens.
- [x] Deprecated cyan aliases and historical hardcoded cyan values are removed
  from JSX/Tailwind usage.
- [x] Remaining cyan hex values are canonical token declarations only.

## Notes

#00c0f9 was the most widely used historical value. HT-012 remains open for
external brand confirmation, but frontend implementation now follows the
canonical design-system token established by HT-306 and migrated in HT-008.

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: resolved by HT-306/HT-008. The frontend now uses `ht-cyan` /
  `ht-cyan-light` and CSS variables rather than historical cyan hex values.
- Verification: `rg "#00c0f9|#19B0F0|#00bfff|customActive|customActiveText|customActiveBlue" src tailwind.config.js`
  returns no active legacy cyan usage.
