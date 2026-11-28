# Deploying to the server

The server runs Jellyfin in Docker. Jellyfin bundles its own copy of the web
client, so to use ours we mount our build over the bundled one.

## Before you deploy

- **The web build must match the server version.** We build from
  `fluffy-moose`, which tracks `release-12.z`, so it's for a 12.x server. If
  the server moves to 13, the web build has to move with it (see
  [upstream-sync.md](upstream-sync.md)).
- **Pin the server image to an exact version**, for example
  `jellyfin/jellyfin:12.4.0` rather than `:latest`, and don't let Watchtower or
  similar update it automatically. Otherwise the server can update underneath
  our web build and the two stop matching.
- **Serve it over HTTPS.** Friends sign in from outside the house, so put a
  reverse proxy with a certificate in front (Caddy and Nginx Proxy Manager both
  get free certificates automatically). Otherwise passwords cross the internet
  unencrypted.

## Steps

1. **Get a build.** Either:
   - download the `fluffy-moose-web` artifact from the latest green run of
     **Fluffy Moose checks** on `fluffy-moose` (Actions tab), or
   - build it yourself: `npm ci && npm run build:production`. The site ends up
     in `dist/`.
2. **Check it isn't empty.** `dist/index.html` must exist. If the mounted
   folder is empty or wrong, Jellyfin refuses to serve the web client at all.
3. **Copy it to the server**, for example to `/opt/fluffy-moose-web`.
4. **Mount it over the bundled web files** and restart the container. The
   path depends on the image:

   | Image | Mount |
   |---|---|
   | Official `jellyfin/jellyfin` | `-v /opt/fluffy-moose-web:/jellyfin/jellyfin-web:ro` |
   | linuxserver.io `lscr.io/linuxserver/jellyfin` | `-v /opt/fluffy-moose-web:/usr/share/jellyfin/web:ro` |

5. **Hard-refresh** the browser (Ctrl+Shift+R). Phones and TVs may need the
   app closed and reopened.

## Rolling back

Remove the mount and restart the container. Jellyfin goes back to its own
bundled web client straight away.

## Styling-only changes: no deploy needed

CSS-only tweaks can go in the server's **Dashboard → Branding → Custom CSS**
box and take effect on the next page load, without a build or a restart.
Keep a copy of whatever goes in there in this repo so it's reviewed and not
lost.
