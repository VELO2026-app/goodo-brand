# Changelog

## 0.4.0 (2026-11-25)

Variant 4 of DSGN-38 (https://linear.app/velo-space/issue/DSGN-38) becomes the
Goodo skin: the look of the native Goodo App (pastel background, 33 px rail),
Goodo's own mood icons, and the brand's own logo instead of the stand-ins.
Three changes in one release, **contract `2.3`**: the old 0.3.2 section below
was never tagged and ships here.

**Order of release.** velo PR VELO2026-app/velo#215 (it reads `assets/mood/`,
contract 2.3) is already in velo's `deploy-machine`; a velo without it refuses
this package (`assets/mood/...: not a file of the skin format`). So: tag
`v0.4.0` on this `main`, then a velo PR raises the pin in
`.github/brand-skins.json` (tag and sha; CI builds and shoots it), then the
instance passport goes last. Without the set (0.3.x) the app draws velo's own
faces.

### Logo (FE-261 №7 and №4, from the designer's Figma vectors)

FE-261 (https://linear.app/velo-space/issue/FE-261): the splash, Welcome and
auth showed a stand-in «GOODO» word and the VELO ring art; the support avatar
and the app icons carried a «G» typeset from Manrope. They are now the
designer's vectors from the Figma file IV92js0q2cBHmHmDxB0zxM, page
«Эксперименты · Goodo»: «Логотип Goodo / индиго» (node 4270:3428), «Логотип
Goodo / белый» (4270:3435), «Знак Goodo / мятный» (4270:3442). The vector paths
are the Figma SVG export, copied as they are; only the wrapper changed (one
`transform` group instead of the export's clip and mask).

- `velo-word-filled.svg` and `velo-word-blue.svg`: the indigo word `#120054`.
  Same box and centre as the stand-in word (402x492 canvas, centre 201, 252;
  299.8 wide in `velo-word-filled.svg`, 166.5 wide in `velo-word-blue.svg`, which
  `VeloLogo` scales 1.8x), so velo's logo calibration is unchanged. Dark, so the
  word reads on the pastel background (the white marks were 1.25:1 there).
- `logo-white.svg`: the white word, same box. The VELO ring that was inside it is
  gone (it was a 318 KB file, now 5 KB).
- `mandala-white.png`, `mandala-blue.png`: fully transparent 492x492 PNGs. The
  logo set must have both ring files (`validate-skin` refuses a half set), but
  the Goodo logo has no ring, so the slot is empty on purpose. The spinning ring
  of the splash is therefore invisible and only the word shows. These were the
  VELO ring art, recoloured; `mandala-white.png` was byte-identical to the golden
  file (the last `validate-skin` warning).
- `favicon.svg`, `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`,
  `apple-touch-icon-180.png`: the mint sign `#A1E0C7` on the ink `#120054`
  (circle for the favicon and the two non-maskable icons, full square for
  the maskable and the touch icon, which stays opaque). The sign is 56 % of the
  side wide; its half diagonal is 0.35 of the side, inside the maskable 80 %
  safe zone (0.4). The favicon is also the support mark (`supportMark: "icon"`).
- Not done here: FE-261 №1 (the onboarding illustrations: the package has no
  `assets/onboarding/` slot content; they come from the designer).
- `validate-skin` (velo `deploy-machine` 359134c9): 0 fail, 0 warn.

### Pastel background and 33 px rail (DSGN-38, was 0.3.2)

See the 0.3.2 section below (PR #5). The known gap it names, white marks on the
pastel background, is closed by the logo above.

### Mood icons (FE-273, PR #6)

FE-273 (https://linear.app/velo-space/issue/FE-273): Goodo's own mood icons in
the check-in and in every other place that shows a mood. Five SVG files and the
contract number; no token or layout change. **The contract is now `2.3`**: the
mood icon set is a new part of the package that a velo reading contract 2.2 or
older refuses (`assets/mood/...: not a file of the skin format`).

- `assets/mood/{bad,low,neutral,good,fire}.svg`: the five icons of the
  check-in scale from the Figma frame «Check-in · вариант 4» (node 4283:2378,
  file IV92js0q2cBHmHmDxB0zxM): a radial glow in the mood's color and the
  hand-drawn face over it. 27-39 KB each, 160 KB in all.
- The lines are `currentColor`: velo draws them in `--velo-primary-dark`, the
  ink `#120054`. In Figma the lines of `good` (dark green `#005409`) and `fire`
  (`#1A1A1A`) have their own colors; they are ink here, one color for all five
  as the task asks. The glow colors stay in the files (they are the mood).
- `viewBox` is the nominal icon box (the Figma frame: 41.6, 51.2 or 64 units);
  the glow runs out of it by 37.5 %, as in the design. velo draws the box at
  the size of the place and lets the glow overflow.
- The files are the Figma export with the coordinates rounded to 0.1 and the
  gradient id renamed to `glow`. Against the original at 3x the render differs
  in at most 19 pixels per icon (each icon is 30 to 70 thousand pixels;
  anti-aliasing), no shape is simplified or dropped. Rounding to 0.01 would
  make the set 65 KB gzip, 0.1 makes it 40 KB.
- `primer-package.yaml`: `contract: "2.3"`.
- `validate-skin` (velo FE-273): 0 fail, 1 warn (the same as 0.3.1).

## 0.3.2 (not tagged; shipped in 0.4.0)

DSGN-38 (https://linear.app/velo-space/issue/DSGN-38): the look of the native
Goodo App (the Calendar screen) on the same velo screens. One asset and one
token; no contract change (the contract stays `2.2`, so this version needs the
same velo as 0.3.1, PR VELO2026-app/velo#203).

- `assets/bg/background.png`: the same mint to lavender gradient as before, with
  a 50 % white veil baked in (pastel). Fitted to the owner's screenshot of the
  Goodo App Calendar: veil t = 0.503, mean absolute error 1.5 of 255 over
  414 thousand background pixels (corners: top left `#C5EFE1`, right edge at
  63 % of the height `#BBBCEA`, bottom right `#C0D2E8`). Size and format are
  unchanged (804x1752, RGBA).
- `tokens/skin.tokens.json`: `velo.rail.pad.x = "33px"` (was the velo default
  24px). The rail is read by MobileLayout, VTabBar, VHeader, CalendarView and
  ChatThreadScreen, so the content and the floating tab bar get the Goodo App's
  336 px content width on a 402 px screen.
- `validate-skin`: 0 fail, 1 warn (the same as 0.3.1).
- Contrast: checked against the darkest and the lightest background pixel under
  every text of eight screens: none below AA, minimum 4.61:1. Known gap: the
  white marks (`logo-white.svg`, `mandala-white.png`) are 1.25:1 on the pastel
  background, so Welcome needs dark variants in those slots (the package already
  has `mandala-blue.png` and `velo-word-blue.svg`; the brand's own logo is still
  to come).

## 0.3.1

FE-261 (https://linear.app/velo-space/issue/FE-261): no «V» in the Goodo
package, and the support conversation's mark is the brand icon, not the VELO
logo set. PM found the VELO letters in the support avatar and on the splash.
Assets plus one brand-record setting; no token or layout change. **The contract
is now `2.2`**: the new field `supportMark` is unknown to a velo that reads
contract 2.1 or older and refused there.

**Order of release: velo needs PR VELO2026-app/velo#203 (it reads `supportMark`,
contract 2.2) before an instance runs this version.** The velo pin in
`.github/brand-skins.json` is raised in that same PR. This is a temporary
stand-in until the brand's own marks arrive: the owner released it as it is.

- Brand record: `"supportMark": "icon"` in `tokens/brand.tokens.json`. The support
  conversation's mark (the header of the support chat at 28 px and the support row
  of the messages list at 40 px) shows the brand's `favicon.svg` instead of the logo
  set. The golden VELO skin does not set it and keeps the logo set there. Splash,
  Welcome and auth do not read it. `primer-package.yaml`: `contract: "2.2"`.
- App icons: `favicon.svg`, `icon-192.png`, `icon-512.png`,
  `icon-maskable-512.png`, `apple-touch-icon-180.png`. The «V» is now a «G»
  in the same colours (mint `#8EE2C6` on ink `#120054`) and the same size
  (40 % of the canvas). `icon-maskable-512.png` keeps the mark inside the 80 %
  safe zone; `apple-touch-icon-180.png` stays opaque (no alpha).
- Wordmark: `velo-word-filled.svg`, `velo-word-blue.svg` and the word inside
  `logo-white.svg` read «GOODO» instead of «VELΘ». Same box and same centre as
  the old word, so velo's logo calibration (`VeloLogo`) is unchanged. The ring
  in `logo-white.svg` is byte-for-byte the old one.
- Both marks are outlines of `assets/fonts/manrope.woff2` (the «G» at weight
  800 plus a 1.6/64 stroke, the word at weight 500). They are placeholders
  until the brand's own marks arrive.
- `mandala-white.png` and `mandala-blue.png` (ring art, no letters) are
  unchanged. `mandala-white.png` is still byte-identical to the golden VELO
  file.
- `validate-skin`: 0 fail, 1 warn (was 2: `velo-word-filled.svg` is no longer
  a golden file). No new golden-identical asset.

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
