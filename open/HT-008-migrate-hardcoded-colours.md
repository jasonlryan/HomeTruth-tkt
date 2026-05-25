# HT-008: Migrate hardcoded frontend colours to canonical tokens

**Priority:** P2
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Goal

Replace hardcoded brand colour values and legacy colour utility names in the
frontend with the canonical HomeTruth `ht.*` Tailwind namespace introduced by
HT-306.

## Description

The frontend now exposes canonical HomeTruth design tokens through Tailwind and
CSS custom properties. The app still contains many hardcoded colours and legacy
aliases such as `primary`, `myblue`, `customActiveText`, `customActiveBlue` and
old cyan/orange/purple hex values.

Migrate brand-colour usages to `ht.*` classes where the intent is clear. Keep
neutral/layout colours only when they are genuinely non-brand UI chrome. Any
unclear colour decision should be logged in the implementation notes rather than
silently guessed.

Depends on HT-306.

## Files

- `src/components/**/*.jsx` — brand colour usages
- `src/pages/**/*.jsx` — brand colour usages
- `src/index.css` — remaining hardcoded brand colour values
- `tailwind.config.js` — remove legacy aliases once no usages remain

## Acceptance Criteria

- [ ] Brand colour JSX usages are migrated to `ht.*` Tailwind classes.
- [ ] Legacy colour utility names are removed from JSX where practical:
  `primary`, `myblue`, `customActive`, `customActiveText`, `customActiveBlue`,
  `customBlue`, `softBlue`, `blurpleLight`.
- [ ] Any remaining hardcoded brand colour values are listed in the
  implementation log with a reason.
- [ ] `tailwind.config.js` retains only compatibility aliases that still have
  active usage, with deprecated aliases clearly marked.
- [ ] `npm run build` passes, or the ticket records why verification could not
  be run.
- [ ] A visual review is performed on the highest-risk changed screens:
  nav/header, auth pages, dashboard, document/chat surfaces and article pages.

## Notes

This is intentionally separate from HT-306. HT-306 created the token bridge;
this ticket performs the migration. Older tickets that mention standardising to
`#00c0f9`, `#19B0F0`, `#00bfff`, `#fd6916` or `#c084fc` should be reconciled
against the canonical design-system tokens before implementation.

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: migrated the first visible slice — navbar, Home Truths listing,
  article detail and resources page brand-colour usages — from hardcoded cyan /
  purple values and `myblue` aliases to canonical `ht.*` Tailwind classes.
- Verification: `npm run build` completed successfully. The build still reports
  existing unused-variable warnings in `KnowledgeBaseAdmin.jsx` and
  `DataPrivacySettings.jsx`; those warnings pre-date this slice.
- Notes: `Resources.jsx` still contains hardcoded neutral/tint layout colours
  such as `#f8fafc`, `#f0f7ff`, `#1e2e5c` and `#111827`. These were left in
  place because this slice only migrated clear brand-colour intent. Remaining
  high-risk surfaces for HT-008 are auth pages, dashboard, document/chat
  surfaces, settings and quiz flows.
