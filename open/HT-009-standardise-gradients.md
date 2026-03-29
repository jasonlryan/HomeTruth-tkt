# HT-009: Standardise gradient definitions

**Priority:** P3
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-03-29

## Description

Create two brand gradient utilities: bg-ht-gradient-warm (orange→pink→purple) and bg-ht-gradient-cool (cyan→blue→purple). Replace ad-hoc gradients.

## Files

- `src/index.css` — add utility classes
- `src/components/FinalCTA.jsx:6`
- `src/pages/AboutUs.jsx:428`
- `src/pages/Pricing.jsx:207`
- `src/pages/Dashboard.jsx:581`
- `src/pages/Documents.jsx:711`

## Acceptance Criteria

- [ ] Two gradient utilities defined
- [ ] All branded gradient sections use one of these two
- [ ] Non-brand gradients (e.g. dark overlays) left as-is

## Notes

FinalCTA currently uses cyan→blue→purple. AboutUs and Pricing use orange→pink→purple. Dashboard and Documents use random Tailwind gradients.
