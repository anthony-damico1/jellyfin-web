# The Fluffy Moose UI

This is a fork of the official Jellyfin web client (jellyfin/jellyfin-web), used to customize the UI on The Fluffy Moose server.

- Work on the **fluffy-moose** branch. It is based on `release-12.z`, which matches our server (Jellyfin 12.4).
- Don't base work on `master`. That is Jellyfin's unreleased dev code and may not work with our server.

## Run it locally

You need Node.js 24+ and npm 11+.

```sh
git clone https://github.com/anthony-damico1/jellyfin-web.git
cd jellyfin-web
git checkout fluffy-moose
npm ci
npm start
```

That starts a dev server (usually http://localhost:8080) that reloads as you edit. When it asks for a server, enter the Jellyfin server's address. On the home network that is http://192.168.1.159:8097. From outside the house you'll need Anthony to give you a remote address or VPN access.

Your changes run in your browser only. Nobody else sees them until they're deployed.

## Where things are

- `src/apps/modern/` - the newer React app: layout, routes and screens (MUI)
- `src/apps/legacy/` - older screens and their controllers
- `src/apps/dashboard/` - the admin dashboard
- `src/components/` - shared UI pieces (cards, home sections, menus, dialogs)
- `src/themes/` - built-in colour themes
- `src/styles/` - global CSS

## Deploying to the server

1. Build: `npm run build:production`. The finished site ends up in `dist/`.
2. Copy `dist/` to the server, for example to `/opt/fluffy-moose-web`.
3. Mount that folder over the container's web files and restart Jellyfin:
   - Official `jellyfin/jellyfin` image: `-v /opt/fluffy-moose-web:/jellyfin/jellyfin-web:ro`
   - linuxserver.io image: `-v /opt/fluffy-moose-web:/usr/share/jellyfin/web:ro`
4. Hard-refresh the browser (Ctrl+Shift+R).

To roll back, remove the mount and restart.

## Updating Jellyfin

Before updating the server, merge the matching upstream release branch into fluffy-moose, then rebuild and redeploy:

```sh
git remote add upstream https://github.com/jellyfin/jellyfin-web.git   # first time only
git fetch upstream
git merge upstream/release-12.z
```

A new major version (e.g. 13) will have a new branch, like `release-13.z`.
