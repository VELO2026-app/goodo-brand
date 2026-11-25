# Goodo — VELO skin package

Source: the Goodo App Figma file, screens Calendar (31:4), Diary map (31:335)
and Analytics / reviews (35:771); the token-by-token comparison with the velo
registry lives on the Figma page `front`, section «Goodo vs velo — token
diff». Converted from the velo skin of generation 1 by
`frontend/scripts/skin-to-dtcg.mjs` (velo FE-131).

```
primer-package.yaml          schema: 1, contract: "2.3" (velo token generation 2; 2.2 = supportMark, 2.3 = mood icons)
tokens/brand.tokens.json     $extensions["velo-skin"]: displayName, shortName,
                             themeColor, backgroundColor, fonts?
tokens/skin.tokens.json      W3C DTCG overrides at the paths of velo's
                             frontend/tokens.json (velo.*, bare.font-body)
assets/                      logo words, empty ring slots, PWA icons, favicon; assets/bg/
assets/mood/                 the five mood icons (bad, low, neutral, good, fire)
```

## Mood icons

`assets/mood/<key>.svg` replace velo's own faces in the check-in and in every
other place that shows a mood (contract 2.3). Source: the Figma frame «Check-in ·
вариант 4» (node 4283:2378). Each file is a radial glow plus the face; the
face lines are `currentColor` (velo draws them in the ink `#120054`), the glow
keeps the mood's own color. `viewBox` is the nominal icon box and the glow runs
out of it. The set is whole or absent: velo refuses four icons of five.

## Palette (ink + mint + lavender)

| name | value | where |
|---|---|---|
| ink | `#120054` | text, primary, outlines, tab-bar disc, Telegram header |
| mint | `#8EE2C6` | screen base (`velo.bg.start`, `velo.tg.bg`), manifest background |
| lavender | `#B1A5FF` | illustrations, analytics "not great" |
| done | `#A1E0C7` on `#005409` | paid / done badge |
| green | `#00AE69` | check mark, analytics "good" |

Background: `assets/bg/background.png` is the mint to lavender gradient with a 50 %
white veil (pastel), as in the Goodo App Calendar screen. Content rail
`velo.rail.pad.x` is 33 px (the Goodo App's 336 px content width).

## Open (owner decisions, not skin data)

- **Font.** The design font Mabry Pro is licensed. Until a licence that
  allows self-hosting arrives, the skin ships Manrope (SIL OFL 1.1, variable
  200-800, Latin + Cyrillic subset; licence text in `skin/LICENSE`), with
  `velo.text.stroke.strong` at `0` because the faux-bold stroke would double
  real weights. Replace `assets/fonts/manrope.woff2`, the `fonts` record and
  `bare.font-body` when Mabry Pro lands.
- **Support mark.** `supportMark: "icon"` in the brand record (contract 2.2):
  the support conversation's mark (support chat header, support row of the
  messages list) is the brand icon `favicon.svg`, not the logo set. The golden
  skin keeps the logo set there. Splash, Welcome and auth do not read it.
- **Marks.** Since 0.4.0 the marks are the designer's vectors (Figma file
  IV92js0q2cBHmHmDxB0zxM, page «Эксперименты · Goodo»): the indigo word in
  `velo-word-filled.svg` and `velo-word-blue.svg` (node 4270:3428), the white
  word in `logo-white.svg` (4270:3435), and the mint sign (4270:3442) on the
  ink in the app icons (`favicon.svg`, `icon-192/512`, `icon-maskable-512`,
  `apple-touch-icon-180`). The vector paths are the Figma SVG export as it is.
  The Goodo logo has no ring, so `mandala-white.png` and `mandala-blue.png`
  are fully transparent (the logo set ships whole or not at all). There is no
  «V» and no VELO art in the package.
- **Secondary text.** The design draws it at 50% ink (3.66:1 on white); the
  contract floor is 4.5:1, so it is 67% (6.66:1).
- The maskable icon's 80% safe zone is a manual check.

## Check

From velo's `frontend/`: `node scripts/validate-skin.mjs <this dir>`, then
`pnpm skin <this dir> && pnpm build`.
