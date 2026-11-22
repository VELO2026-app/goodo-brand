# Goodo — VELO skin package

Source: the Goodo App Figma file, screens Calendar (31:4), Diary map (31:335)
and Analytics / reviews (35:771); the token-by-token comparison with the velo
registry lives on the Figma page `front`, section «Goodo vs velo — token
diff». Converted from the velo skin of generation 1 by
`frontend/scripts/skin-to-dtcg.mjs` (velo FE-131).

```
primer-package.yaml          schema: 1, contract: "2.0" (velo token generation 2)
tokens/brand.tokens.json     $extensions["velo-skin"]: displayName, shortName,
                             themeColor, backgroundColor, fonts?
tokens/skin.tokens.json      W3C DTCG overrides at the paths of velo's
                             frontend/tokens.json (velo.*, bare.font-body)
assets/                      logos, PWA icons, favicon; assets/bg/
```

## Palette (ink + mint + lavender)

| name | value | where |
|---|---|---|
| ink | `#120054` | text, primary, outlines, tab-bar disc, Telegram header |
| mint | `#8EE2C6` | screen base (`velo.bg.start`, `velo.tg.bg`), manifest background |
| lavender | `#B1A5FF` | illustrations, analytics "not great" |
| done | `#A1E0C7` on `#005409` | paid / done badge |
| green | `#00AE69` | check mark, analytics "good" |

## Open (owner decisions, not skin data)

- **Font.** The design font Mabry Pro is licensed. Until a licence that
  allows self-hosting arrives, the skin ships Manrope (SIL OFL 1.1, variable
  200-800, Latin + Cyrillic subset; licence text in `skin/LICENSE`), with
  `velo.text.stroke.strong` at `0` because the faux-bold stroke would double
  real weights. Replace `assets/fonts/manrope.woff2`, the `fonts` record and
  `bare.font-body` when Mabry Pro lands.
- **Marks.** Logo shapes are still the VELO ones (wordmark, V, mandala),
  recoloured to the Goodo palette; the real Goodo marks come from the brand.
- **Secondary text.** The design draws it at 50% ink (3.66:1 on white); the
  contract floor is 4.5:1, so it is 67% (6.66:1).
- The maskable icon's 80% safe zone is a manual check.

## Check

From velo's `frontend/`: `node scripts/validate-skin.mjs <this dir>`, then
`pnpm skin <this dir> && pnpm build`.
