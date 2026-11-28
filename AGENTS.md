# Agent rules for this fork

This is **The Fluffy Moose** fork of Jellyfin Web. Start with
`.github/README.md` and `docs/fluffy-moose/`.

## Hard rules

- **Work on `fluffy-moose`, never `master`.** `fluffy-moose` tracks Jellyfin's
  `release-12.z`, which matches the server. `master` is Jellyfin's unreleased
  development code. Branch as `fluffy/<topic>` and open PRs into `fluffy-moose`.
- **Node 24+ and npm 11+.** `.npmrc` has `engine-strict=true`, so older
  versions fail with `EBADENGINE`. On the Fedora dev box, put
  `~/.local/node24/bin` first on `PATH`.
- **Keep the fork's footprint small.** Put fork work in new files
  (`src/themes/fluffymoose/`, `docs/fluffy-moose/`, `.github/workflows/fluffy-*.yml`,
  `.github/README.md`). Every line changed in a Jellyfin file is a future
  merge conflict for the weekly upstream sync. Never edit the root `README.md`.
- **The repo is public.** Never commit server addresses (LAN or public),
  credentials, or anything else from the server's configuration.
- **Never copy game assets.** The theme is *inspired by* old-school fantasy
  MMOs. No logos, sprites, icons, fonts, sounds or names from any real game.
  Fonts must be open-licensed and bundled through `@fontsource`.
- **Follow the style guide** (`docs/fluffy-moose/style-guide.md`):
  - Text contrast must pass WCAG AA.
  - The pixel font is for labels only, never in paragraphs or on buttons, and
    it never renders digits.
  - No text on the progress bar.

## Before opening a PR

Run what CI runs (`.github/workflows/fluffy-checks.yml`):

```sh
npm run build:check && npm run lint && npm run stylelint && npm test && npm run build:production
```

If you touch `.github/workflows/`, also run `actionlint` on the changed files.
