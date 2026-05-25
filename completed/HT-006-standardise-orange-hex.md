# HT-006: Standardise orange to single hex value

**Priority:** P3
**Repo:** frontend
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

Two orange values were used: #fd6916 (primary) and #e65a0c (hover). This
ticket originally proposed keeping that pair, but it has been superseded by the
canonical HomeTruth design-system tokens `--ht-orange: #E8651A` and
`--ht-orange-light: #F28C4E`.

## Files

- `src/components/WhoWeHelp.jsx`
- `src/pages/Pricing.jsx`

## Acceptance Criteria

- [x] Orange brand usage is centralised through canonical `ht.*` tokens.
- [x] Historical hardcoded orange values are removed from JSX/Tailwind usage.
- [x] Remaining orange hex values are canonical token declarations only.

## Notes

Relatively minor — historical orange values served normal/hover purposes. The
canonical normal/hover pair is now owned by the design-system token bridge.

## Implementation Log

### 2026-05-25

- Repo: frontend
- Changed: resolved by HT-306/HT-008. The frontend now uses `ht-orange` /
  `ht-orange-light` and CSS variables rather than historical orange hex values.
- Verification: `rg "#fd6916|#FD6916|#e65a0c|#E65A0C" src tailwind.config.js`
  returns no active historical orange usage.
