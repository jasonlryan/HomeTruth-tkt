# HT-012: Resolve brand colour hex values by provenance

**Priority:** P2
**Repo:** design-system
**Created:** 2026-03-29
**Updated:** 2026-05-25

## Description

The style guide marks all colour swatches as `TBC` and includes a page 7 note
to "Change purple throughout". Rather than leaving product implementation
blocked on external confirmation, resolve the current brand decisions by
provenance: use the strongest explicit, current source for product UI tokens,
while preserving approved logo/artwork colours as artwork-specific values.

## Files

- `design-system/foundations/brand-provenance.md`
- `design-system/foundations/colour.md`
- `design-system/logos/README.md`
- `design-system/tokens/tokens.json`
- `design-system/tokens/tokens.css`

## Acceptance Criteria

- [x] Confirmed provenance-based UI hex values for: HT Orange, HT Purple,
  HT Blue/Cyan, HT Green.
- [x] Clarity on how to treat the page 7 "Change purple throughout" note.
- [x] Source hierarchy is documented so future brand decisions can be traced.
- [x] Logo/artwork colours are explicitly separated from product UI tokens.

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
`design-system/tokens/tokens.css` and the frontend token bridge.

Provenance decision:

- `hometruth DOCS/BRAND.md`, `hometruth DOCS/CLAUDE.md` and the product token
  bridge are explicit current sources for product UI colours.
- `brand-and-style/HomeTruth Development Style Guide 14.08.pdf` establishes
  palette names and visual direction, but page 10 marks swatches as `TBC`.
- Approved logo/icon assets carry artwork-specific values such as orange
  `#FD6815`, purple `#7B4B9E` and cyan `#19B0F0`; these stay in artwork and do
  not override product UI tokens.
- The page 7 "Change purple throughout" note is unspecific. Until a more
  explicit source exists, it does not change UI purple or trigger logo
  recolouring.

## Implementation Log

### 2026-05-25

- Repo: n/a
- Changed: updated this ticket with the canonical values currently implemented
  in the design-system and frontend.
- Verification: not complete. This is blocked on external BrandAd confirmation
  and remains open.

### 2026-05-25

- Repo: design-system
- Changed: resolved brand colour decisions by provenance rather than waiting
  for an external confirmation loop. Added `foundations/brand-provenance.md`
  and updated design-system, colour, logo and token docs to state the source
  hierarchy.
- Verification: local evidence reviewed:
  `hometruth DOCS/BRAND.md`, `hometruth DOCS/CLAUDE.md`, the frontend token
  bridge, design-system tokens, logo/icon SVG artwork and the style-guide PDF
  text. The style-guide PDF page 10 marks colour values as `TBC`; sampled
  swatches align more closely with artwork values than the UI token set, so
  they are treated as supporting evidence rather than final UI hex values.
- Decision: keep current product UI values (`#E8651A`, `#00B4D8`, `#8B3FA0`,
  `#43B02A`); keep embedded artwork colours in logo/icon files; require a new
  ticket with explicit source evidence for any future full-palette replacement.
