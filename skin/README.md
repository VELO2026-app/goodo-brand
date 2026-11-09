# Goodo — VELO skin package

Source: the Goodo App Figma file, screens Calendar (31:4), Diary map (31:335)
and Analytics / reviews (35:771); the token-by-token comparison with the velo
registry lives on the Figma page `front`, section «Goodo vs velo — token
diff». Converted from the velo skin of generation 1 by
`frontend/scripts/skin-to-dtcg.mjs` (velo FE-131).

```
primer-package.yaml          schema: 1, contract: "1.0"
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

- **Font.** Mabry Pro is a licensed face. A package ships its font as a file
  (`assets/fonts/*.woff2`, listed under `fonts` in `brand.tokens.json`,
  named in `bare.font-body`) — no external font URL. Needs a licence that
  allows self-hosting. Until then the skin keeps Marmelad. When it lands,
  also set `velo.text.stroke.strong` to `0` (Marmelad's faux-bold stroke
  would double the real Medium weight).
- **Marks.** Logo shapes are still the VELO ones (wordmark, V, mandala),
  recoloured to the Goodo palette; the real Goodo marks come from the brand.
- **Secondary text.** The design draws it at 50% ink (3.66:1 on white); the
  contract floor is 4.5:1, so it is 60% (5.18:1).
- The maskable icon's 80% safe zone is a manual check.

## Check

From velo's `frontend/`: `node scripts/validate-skin.mjs <this dir>`, then
`pnpm skin <this dir> && pnpm build`.
