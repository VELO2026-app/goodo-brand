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

Releases are tags; a released tag is never moved -- an instance goes back to
a look by its tag. The format and its checks are defined by the product:
velo `tz-whitelabel.md` §3 / §3.2, engine `frontend/scripts/lib/skin-package.mjs`.
