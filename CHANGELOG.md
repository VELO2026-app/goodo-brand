# Changelog

## 0.3.0 (not tagged yet)

FE-193: bring the Goodo skin closer to the designer's mockups (Figma page
«Эксперименты · Goodo») and lift the text/background pairs to WCAG AA.
Tokens only; no layout and no asset changes.

Requires velo with the FE-193 tokens (velo PR "FE-193 semantic tokens"):
`validate-skin` refuses a token path the product does not know, so this
version does not build on an older velo. Contract stays `2.0`.

New overrides (the 11 velo FE-193 tokens):
- `frost.border` ink, `frost.bg` ink 15% — tab bar and composer: ink outline
  and ink-tinted glass instead of the white-glass frame.
- `control.border` ink — segment and practice-picker pill outlines.
- `on.primary` mint `#8EE2C6` — tab-bar disc, active segment, composer send.
- `picker.bg` transparent, `picker.fg` ink — the practice-picker pill is an
  outlined pill, as in the mockups.
- `back.bg` ink, `back.fg` mint, `back.glass.bg` ink — back button.
- `text.on.bg.secondary`, `text.on.bg.muted` ink 82% — text drawn on the
  screen gradient (4.5:1 on its darkest lavender zone).

Contrast fixes of golden palette steps the skin had not covered:
- `text.muted` 50% → 58% ink (4.5:1 on white), `text.secondary` 60% → 67%
  (4.5:1 on the light-blue cards and rows).
- `pink.300` `#B3283F` (white text on danger buttons 2.15 → 6.4:1; text on
  the pink tint 1.75 → 5.2:1), `pink.700` `#7A2230`, `glass.pink.40` a light
  tint, so the alert banner keeps dark text on a light fill.
- `peach.500` `#5B3714`, `peach.700` `#8A5320`, `peach.800` `#9A4709`:
  warning text on peach fills (1.26 → 4.6:1 and 4.1 → 5.2:1).

Not done (needs the owner or the designer): the brand font (Mabry Pro), real
Goodo marks, date-bracket and tab-bar shapes. See the FE-193 report.

## 0.2.0
Contract 2.0 for velo token generation 2 (FE-150).
## 0.1.1
Mint screen base, machine-form slot example.
## 0.1.0
First Goodo skin package, DTCG from the Goodo App design.
