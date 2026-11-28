# The Fluffy Moose: Jellyfin web client

Our customised web interface for **The Fluffy Moose**, a Jellyfin media server
shared by a group of friends. It's a fork of the official
[Jellyfin Web](https://github.com/jellyfin/jellyfin-web) client (GPL-2.0),
restyled with an old-school fantasy MMO look, **Stone & Gold**, and a cleaner,
easier-to-navigate layout.

![Stone & Gold home screen](https://imgup-mockups-e96317512e4b.s3.us-east-1.amazonaws.com/images/2026/11/1b0e13a8713440c187d9.png)

## What this repo is for

1. **Restyle the UI** for our server: theme, layout and a few nostalgic touches.
2. **Keep getting Jellyfin's updates** without our changes breaking. A weekly
   Action merges Jellyfin's release branch, runs every check, and opens a PR.
3. **Deploy** a tested build to the server, matched to its Jellyfin version.

It is *not* the server, and it doesn't change how media is stored or streamed.
It's only the website you use to browse and play.

## Branches

| Branch | What it is |
|---|---|
| **`fluffy-moose`** | Our version. Based on Jellyfin's `release-12.z`, matching our 12.4 server. **All work goes here, through pull requests.** |
| `master` and `release-*` | Jellyfin's own branches, copied when the repo was forked. Don't build on `master`: it's unreleased 13.x code. |
| `sync/upstream` | Made by the weekly update Action. Merge its PR to take Jellyfin's fixes. |

## Docs

| Doc | For |
|---|---|
| [First-time setup checklist](../docs/fluffy-moose/anthony-checklist.md) | Repo owner: one-off GitHub settings |
| [Developing](../docs/fluffy-moose/development.md) | Running it locally, where things are, checks |
| [Style guide](../docs/fluffy-moose/style-guide.md) | The Stone & Gold look: colours, fonts, decisions, screenshots |
| [Staying up to date](../docs/fluffy-moose/upstream-sync.md) | How Jellyfin's updates flow in, and what to do when it fails |
| [Deploying](../docs/fluffy-moose/deploying.md) | Getting a build onto the server, and rolling back |

Jellyfin's own README is still at the [repo root](../README.md). GitHub shows
this file instead because it's in `.github/`, so we never have to edit
Jellyfin's README and their updates can't conflict with ours.

## Licence

GPL-2.0-or-later, the same as Jellyfin Web. See [LICENSE](../LICENSE).
