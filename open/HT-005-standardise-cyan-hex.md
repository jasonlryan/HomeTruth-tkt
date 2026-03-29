# HT-005: Standardise cyan to single hex value

**Priority:** P2
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-03-29

## Description

Three different cyan values are used: #00c0f9, #00bfff, and #19B0F0. Standardise all to #00c0f9.

## Files

- `src/components/Navbar.jsx` — 4 instances of #00bfff
- `src/index.css` — #19B0F0 in bullet SVG
- `src/components/AttitudinalQuizModal.jsx` — #19B0F0F0
- `tailwind.config.js` — customActive/customActiveText/customActiveBlue all use #19B0F0 variants

## Acceptance Criteria

- [ ] Only #00c0f9 appears in codebase for cyan
- [ ] Hover state standardised to #00ace0

## Notes

#00c0f9 is the most widely used value. Confirm with BrandAd (HT-012) if this is the final colour.
