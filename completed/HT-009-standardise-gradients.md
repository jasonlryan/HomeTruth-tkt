# HT-009: Standardise gradient definitions

**Priority:** P3
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Create two brand gradient utilities: `bg-ht-gradient-warm` and
`bg-ht-gradient-cool`. Replace repeated ad-hoc branded gradients while leaving
non-brand overlays and neutral decoration alone.

## Files

- `src/index.css` — add utility classes
- `src/components/FinalCTA.jsx:6`
- `src/pages/AboutUs.jsx:428`
- `src/pages/Pricing.jsx:207`
- `src/pages/Dashboard.jsx:581`
- `src/pages/Documents.jsx:711`

## Acceptance Criteria

- [x] Two gradient utilities defined
- [x] All branded gradient sections use one of these two
- [x] Non-brand gradients (e.g. dark overlays) left as-is

## Notes

Because the canonical token set does not include pink or blue primitives, the
implemented utilities use available HomeTruth tokens:
`bg-ht-gradient-warm` = orange → purple-light → purple, and
`bg-ht-gradient-cool` = cyan → cyan-light → purple.

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: added `bg-ht-gradient-warm` and `bg-ht-gradient-cool` utilities in
  `src/index.css`. Replaced branded CTA gradients in `FinalCTA.jsx`,
  `AboutUs.jsx` and `Pricing.jsx` with the warm utility. Replaced dashboard
  upload and documents banner gradients with the cool utility.
- Verification: `rg "bg-gradient-to-r from-ht|from-ht-cyan|from-ht-orange|bg-ht-gradient" src`
  shows branded gradient usage has moved to the named utilities. Remaining
  Tailwind gradients are non-brand overlays, article placeholders, pseudo
  underlines or neutral decoration. `npm run build` completed successfully with
  the existing warnings.
