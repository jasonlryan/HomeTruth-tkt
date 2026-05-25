# HT-001: Load Gill Sans web font

**Priority:** P1
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Add Gill Sans .woff2 font files (Light 300, Regular 400, Bold 700) to
`/public/fonts/` and declare `@font-face` rules in `src/index.css`.
`font-display: swap` is required for performance.

## Files

- `src/index.css` — add @font-face declarations
- `public/fonts/` — new directory for font files
- `tailwind.config.js` — prefer the self-hosted family in `font-brand`
- `design-system/tokens/*` and `design-system/foundations/typography.md` —
  keep canonical typography tokens aligned

## Acceptance Criteria

- [x] @font-face rules for 3 weights (Light 300, Regular 400, Bold 700)
- [x] Fonts load in browser
- [x] Fallback to system fonts if missing
- [x] Font-display: swap applied for performance

## Notes

Gill Sans is a licensed font — need .woff2 files from existing font files on Jason's Mac. macOS ships with Gill Sans so can convert from system font. Style guide specifies Light, Regular, Bold weights.

Confirm web embedding rights before distributing the generated font files
outside authorised project repositories.

## Implementation Log

### 2026-05-25

- Repos: frontend, design-system
- Changed: generated `gill-sans-light.woff2`, `gill-sans-regular.woff2` and
  `gill-sans-bold.woff2` from the local macOS Gill Sans collection and added
  them under `public/fonts/`. Added matching `@font-face` rules to
  `src/index.css`, updated `--font-base`, and made Tailwind `font-brand` prefer
  `"HomeTruth Gill Sans"` before local/system fallbacks. Updated design-system
  typography tokens and docs to match.
- Verification: `npm run build` completed successfully. The build still reports
  the existing unused-variable warnings in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`, plus the existing outdated Browserslist notice.
  Local font URLs under `/fonts/*.woff2` returned HTTP 200 with
  `Content-Type: font/woff2`, and the landing page rendered in the browser.
- Notes: the production build emits hashed WOFF2 assets from the CSS import and
  also copies `public/fonts/` into `build/fonts/`; this is acceptable for now
  because the source-of-truth files remain in `public/fonts/`.
