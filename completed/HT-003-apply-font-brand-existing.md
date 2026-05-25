# HT-003: Apply font-brand to existing font-gill components

**Priority:** P1
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Update the 4 files currently using font-gill class to use the new font-brand class instead.

## Files

- `src/components/Navbar.jsx:27`
- `src/pages/HomeTruths.jsx:60`
- `src/pages/Resources.jsx:38`
- `src/pages/ArticleDetail.jsx:50`

## Acceptance Criteria

- [x] All 4 files use font-brand
- [x] No remaining references to font-gill in codebase

## Notes

Simple find-and-replace: font-gill → font-brand

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: reconciled ticket state against the current frontend baseline.
  `Navbar.jsx`, `HomeTruths.jsx`, `Resources.jsx` and `ArticleDetail.jsx`
  already use `font-brand`, and no `font-gill` references remain.
- Verification: `rg "font-gill|font-brand" src tailwind.config.js` confirms no
  `font-gill` usage and active `font-brand` usage on the listed files.
