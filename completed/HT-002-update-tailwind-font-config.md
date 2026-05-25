# HT-002: Update tailwind font config

**Priority:** P1
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Replace current font-gill/font-inter/font-sans entries in tailwind.config.js
with font-brand (Gill Sans + fallbacks) and font-chat (system-ui stack).
Remove Inter dependency from package.json if unused elsewhere.

## Files

- `tailwind.config.js` — lines 9-13
- `package.json` — remove Inter if unused

## Acceptance Criteria

- [x] font-brand class renders Gill Sans
- [x] font-chat class renders system-ui stack
- [x] No references to old font-gill/font-inter remain

## Notes

Fallback stack for brand is now owned by HT-001 and the design-system
typography token: `"HomeTruth Gill Sans", "Gill Sans", "Gill Sans MT",
-apple-system, "Helvetica Neue", Arial, sans-serif`.

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: removed the unused `@fontsource/inter` dependency from
  `package.json` / `package-lock.json`, removed the old Tailwind `inter` font
  alias, and removed the backward-compatible `.font-inter` CSS rule. Kept
  canonical `font-brand` and `font-chat` only.
- Verification: `rg "@fontsource/inter|font-inter|font-gill|inter:" src public package.json package-lock.json tailwind.config.js`
  returns no matches. `rg "font-brand|font-chat|fontFamily" src tailwind.config.js`
  confirms the active brand/chat font surfaces. `npm run build` completed
  successfully with the existing unused-variable warnings in
  `KnowledgeBaseAdmin.jsx` and `DataPrivacySettings.jsx`, plus the existing
  outdated Browserslist notice.
