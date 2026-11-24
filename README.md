# goodo-brand

The Goodo brand for VELO instances: data packages of the deploy machine
`pridem` (PRIMER-PROTOCOL 1.4, contract 3 rule 10). No code, no instance
values; which version an instance shows is in its passport.

```
skin/     the look -- slot packages.skin of velo (apply: build)
texts/    (later) terminology overlays -- slot texts of velo (FE-133)
```

Each subdirectory carries its own `primer-package.yaml`; ONE tag `vX.Y.Z`
versions them together, and both slots of an instance take this repository
by that tag through `subpath` in the passport (the form of the machine's
reference `primer-blank-brand`; `subpath` is required -- the repository root
is not a package):

```yaml
packages:
  skin: { repo: git@github.com:VELO2026-app/goodo-brand.git, version: 0.2.0, subpath: skin }
```

The repository is private: the machine reads it with its deploy key.

Version 0.3.0 needs velo >= PR VELO2026-app/velo#175 (new skin tokens, `validate-skin` refuses unknown paths). Order: merge velo#175 first, then tag. The example above changes to the new version together with the tag.

## TODO

- **Support address** (velo FE-251, contract `2.2`): the address will come from
  the owner. Until then the brand record has no `supportEmail`, and the support
  screens of a Goodo instance show no address line, the same as the core build
  without a package. With the address: `supportEmail` in
  `skin/tokens/brand.tokens.json`, `contract: "2.2"` in
  `skin/primer-package.yaml`, a new tag, then velo raises its CI pin.

Releases are tags; a released tag is never moved -- an instance goes back to
a look by its tag. The format and its checks are defined by the product:
velo `tz-whitelabel.md` §3 / §3.2, engine `frontend/scripts/lib/skin-package.mjs`.
