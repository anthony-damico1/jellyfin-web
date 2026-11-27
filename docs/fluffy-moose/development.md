# Developing the Fluffy Moose UI

## Which branch

- Work on **`fluffy-moose`**. It's based on Jellyfin's `release-12.z` branch,
  which matches our server (Jellyfin 12.4).
- Don't base work on `master`. That's Jellyfin's unreleased development code
  (13.x), and it may not work with our server.
- Make a branch for each change (`git switch -c fluffy/<what-it-does>`) and
  open a pull request into `fluffy-moose`. The checks run on every PR.

## Run it locally

You need **Node.js 24+ and npm 11+**. The project refuses to install on
anything older (`EBADENGINE`).

- **Fedora:** `sudo dnf install nodejs24 nodejs24-npm`. This installs
  `node-24` and `npm-24` alongside your existing Node without replacing it.
  To use them for this repo, put shims first on your `PATH`:

  ```sh
  mkdir -p ~/.local/node24/bin
  ln -sf /usr/bin/node-24 ~/.local/node24/bin/node
  ln -sf /usr/bin/npm-24  ~/.local/node24/bin/npm
  ln -sf /usr/bin/npx-24  ~/.local/node24/bin/npx
  export PATH="$HOME/.local/node24/bin:$PATH"   # in each shell you use for this repo
  ```

- **Other systems:** any Node 24 install works (nodejs.org, `fnm`, `nvm`).
  The version is pinned in `.nvmrc`.

Then:

```sh
git clone https://github.com/anthony-damico1/jellyfin-web.git
cd jellyfin-web
git switch fluffy-moose
npm ci
npm start
```

That starts a dev server (usually <http://localhost:8080>) that reloads as you
edit. When it asks for a server, enter our Jellyfin server's address. Anthony
can give you the LAN or remote address. Don't commit server addresses to this
repo, because it's public.

Your changes only run in your browser. Nobody else sees them until they're
deployed.

## Checks to run before opening a PR

These are the same commands CI runs:

```sh
npm run build:check   # TypeScript
npm run lint          # ESLint
npm run stylelint     # CSS/SCSS
npm test              # Vitest
npm run build:production
```

## Where things are

| Path | What |
|---|---|
| `src/apps/modern/` | The newer React app: layout, toolbar, side drawer, routes (MUI) |
| `src/apps/legacy/` | Older screens and their controllers |
| `src/apps/dashboard/` | The admin dashboard |
| `src/components/` | Shared UI pieces: cards, home sections, menus, dialogs |
| `src/components/homesections/` | The home page rows (Continue Watching, Next Up, …) |
| `src/themes/` | Colour themes. Each one has a `theme.scss` and a MUI colour scheme in `index.ts` |
| `src/themes/_base/` | Shared theme base and the default MUI palette |
| `src/styles/` | Global CSS |
| `src/config.json` | Theme list, plugins, menu links |

## Keeping our changes easy to merge

Jellyfin's updates merge in automatically every week (see
[upstream-sync.md](upstream-sync.md)). Every line we change in Jellyfin's own
files is a line that can conflict with theirs. So:

- Put new things in **new files**: our theme goes in `src/themes/fluffymoose/`,
  and fork docs go in `docs/fluffy-moose/`.
- When you have to edit an existing Jellyfin file, keep the change small and
  in as few places as possible.
- Styling that the server's **Custom CSS** box (Dashboard → Branding) can do
  doesn't need a code change at all.
