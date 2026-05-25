# HT-012: Confirm brand colour hex values with BrandAd

**Priority:** P2
**Repo:** n/a
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

The style guide marks ALL colours as "TBC" (to be confirmed). Get final hex values from Bill Wallsgrove at BrandAd. Also clarify the "Change purple throughout" note on page 7.

## Files

- n/a — this is a communication task

## Acceptance Criteria

- [ ] Confirmed hex values for: HT Orange, HT Purple, HT Blue/Cyan, HT Green
- [ ] Clarity on purple change

## Notes

Current canonical implementation values are:

- HT Orange: `#E8651A`
- HT Orange Light: `#F28C4E`
- HT Cyan: `#00B4D8`
- HT Cyan Light: `#48D1E8`
- HT Purple: `#8B3FA0`
- HT Purple Light: `#A966BF`
- HT Green: `#43B02A`
- HT Green Light: `#6BC955`

These are implemented in `design-system/tokens/tokens.json`,
`design-system/tokens/tokens.css` and the frontend token bridge. They still
need external confirmation from BrandAd before being treated as final.

## External Confirmation Brief

Ask BrandAd to confirm:

- Final hex values for HT Orange, HT Purple, HT Blue/Cyan and HT Green.
- Whether light/hover variants should be fixed brand values or generated
  tints.
- What exactly the style-guide p7 note "Change purple throughout" refers to:
  the TH icon only, the full wordmark, all UI purple tokens or another asset
  family.
- Whether existing logo/icon files need regeneration after purple confirmation.

## Implementation Log

### 2026-05-25

- Repo: n/a
- Changed: updated this ticket with the canonical values currently implemented
  in the design-system and frontend.
- Verification: not complete. This is blocked on external BrandAd confirmation
  and remains open.
