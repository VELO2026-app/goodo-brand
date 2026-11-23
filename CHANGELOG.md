# Changelog

## 0.3.0

FE-193 (https://linear.app/velo-space/issue/FE-193): bring the Goodo skin
closer to the designer's mockups (Figma page «Эксперименты · Goodo») and lift
text/background pairs to WCAG AA. Tokens, one font file; no layout change,
no new image assets. Contract stays `2.0`.

**Order of release: merge VELO2026-app/velo#175 first, then tag.** The package
uses velo tokens that exist only after that PR (`validate-skin` refuses an
unknown token path), so 0.3.0 does not build on an older velo. Nothing in the
contract number guards this; the order does.

Overrides of the new velo tokens (velo#175):
- `frost.border`, `frost.border.active`, `frost.bg`, `frost.bg.active`: tab bar
  and composer — ink outline and ink-tinted glass instead of the white frame.
- `control.border`: segment and practice-picker outlines, ink.
- `on.accent`: mint `#8EE2C6` on accent fills (tab-bar disc, active segment,
  composer send), 12.0:1 on ink.
- `picker.bg` transparent, `picker.fg` ink: outlined practice-picker pill.
- `back.button.bg`, `back.button.glass.bg` ink, `back.button.fg` mint.
- `text.on.bg.secondary`, `text.on.bg.muted`: opaque ink for text drawn on the
  screen gradient — 4.7:1 on its darkest lavender zone (82% ink gave 3.9:1).

Look:
- Font: Manrope (SIL OFL 1.1, variable 200-800, Latin + Cyrillic subset,
  38 KB, `skin/LICENSE`); `text.stroke.strong` 0. It stands in for
  Mabry Pro, which needs a licence that allows self-hosting.
- `shadow.glow`, `shadow.glow.sm` none and `shadow.glass` a soft ink shadow:
  the white glow and white glass highlights are not in the mockups.

Contrast (golden palette steps the skin had not covered):
- `text.muted` 50% → 58% ink (4.8:1 on white); `text.secondary` 60% → 67%
  (6.7:1 on white).
- `pink.300` `#B3283F`: white text on danger buttons 2.15 → 6.4:1, text on the
  light pink tint 1.75 → 5.2:1. `pink.700` `#6A1D2A` (error banner title on the gradient, 4.9:1). `glass.pink.40` a light
  tint so the alert banner keeps dark text on a light fill.
- Warning banner lies directly on the gradient (fill: peach-300 at 40%; worst
  case over the darkest lavender, about `#AB95B6`): `peach.700` `#4C2E12`
  (title and icon, was 2.3:1) and `peach.500` `#4A2D10` (body, was 3.8:1),
  both 4.5:1 or better there.
- Success banner (teal-300 glass at 40% over the same zone): `teal.700` `#143D40`
  (title, was 2.0:1) and `teal.600` `#003A06` (body, was 3.5:1, now 5.0:1). `teal.600` is
  a shared step (about 20 consumers: success badge and stat-card text, diary
  card text, three dots and fills); `#005409` → `#003A06` is a slight
  darkening of the same deep green, accepted.

Shared palette steps: `pink.300` and `peach.500` are shared steps, so more than
the targeted text changes. Consumers found by grep and the key screens looked at; accepted:
- `--velo-error` border: crimson instead of pink.
- booking-status dot on the dashboard card (`UserDashboardView`): crimson.
- admin tab-bar badge: white on crimson (6.4:1).
- support topic «tech» icon and support-ticket accents: crimson / brown.
- rating-sheet filled stars (`SupportRatingSheet`): brown `#4A2D10` instead of
  orange — readable, not pretty; the star colour is a design decision.
- «Log an activity» quick card (peach glass): brown text; same decision.
The Goodo palette has no warm accent, so a designed warning/error palette is
the real fix (FE-193 report, designer brief).

Not in the package (needs the owner or the designer): the brand font itself,
real Goodo marks, tab-bar disc and back-button shapes, practice-card layout.

## 0.2.0
Contract 2.0 for velo token generation 2 (FE-150).
## 0.1.1
Mint screen base, machine-form slot example.
## 0.1.0
First Goodo skin package, DTCG from the Goodo App design.
