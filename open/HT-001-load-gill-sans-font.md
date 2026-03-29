# HT-001: Load Gill Sans web font

**Priority:** P1
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-03-29

## Description

Add Gill Sans .woff2 font files (Light 300, Regular 400, Bold 700) to /public/fonts/ and declare @font-face rules in src/index.css. Font-display: swap for performance.

## Files

- `src/index.css` — add @font-face declarations
- `public/fonts/` — new directory for font files

## Acceptance Criteria

- [ ] @font-face rules for 3 weights (Light 300, Regular 400, Bold 700)
- [ ] Fonts load in browser
- [ ] Fallback to system fonts if missing
- [ ] Font-display: swap applied for performance

## Notes

Gill Sans is a licensed font — need .woff2 files from existing font files on Jason's Mac. macOS ships with Gill Sans so can convert from system font. Style guide specifies Light, Regular, Bold weights.
