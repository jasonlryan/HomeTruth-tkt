# HT-002: Update tailwind font config

**Priority:** P1
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-03-29

## Description

Replace current font-gill/font-inter/font-sans entries in tailwind.config.js with font-brand (Gill Sans + fallbacks) and font-chat (system-ui stack). Remove Inter dependency from package.json if unused elsewhere.

## Files

- `tailwind.config.js` — lines 9-13
- `package.json` — remove Inter if unused

## Acceptance Criteria

- [ ] font-brand class renders Gill Sans
- [ ] font-chat class renders system-ui stack
- [ ] No references to old font-gill/font-inter remain

## Notes

Fallback stack for brand: "Gill Sans", "Gill Sans MT", Calibri, sans-serif
