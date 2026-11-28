# Staying up to date with Jellyfin

We want Jellyfin's fixes without our changes breaking. A GitHub Action does
most of the work.

## What runs automatically

**Upstream sync** (`.github/workflows/fluffy-upstream-sync.yml`) runs every
Monday and can also be started by hand (Actions → Upstream sync → Run
workflow). It:

1. Fetches Jellyfin's `release-12.z` branch and checks for commits we don't have yet.
   If there are none, it stops: "already up to date".
2. Merges them into a fresh `sync/upstream` branch made from `fluffy-moose`.
3. Runs the full set of checks on the merged code: TypeScript, ESLint,
   Stylelint, the tests and a production build.
4. Opens (or updates) a pull request from `sync/upstream` into `fluffy-moose`,
   listing Jellyfin's new commits.

If the merge conflicts with our changes, or any check fails, **the run fails
and GitHub emails the repo watchers.** Nothing reaches `fluffy-moose` until
someone merges the PR.

It also checks whether Jellyfin has started a **newer release branch**, for
example `release-13.z`. If so, that job fails on purpose, to remind us. A new
major version isn't merged automatically, because the server and the web client
have to be upgraded together.

**Fluffy Moose checks** (`.github/workflows/fluffy-checks.yml`) runs the same
checks on every pull request into `fluffy-moose` and every push to it. Builds
of `fluffy-moose` upload the finished site as the `fluffy-moose-web` artifact,
ready to deploy.

GitHub pauses scheduled workflows in a public repo after 60 days with no
activity. If the weekly run stops appearing, open Actions → Upstream sync and
click **Enable workflow**.

## Why the sync runs its own checks

A pull request opened by an Action using GitHub's built-in token doesn't
trigger other workflows. That's a GitHub rule to stop runaway loops. So
"Fluffy Moose checks" won't run on the sync PR by itself. The sync workflow
runs the checks before opening the PR, and the PR links to that run.

If you turn on *required status checks* in branch protection, the sync PR won't
have them. Close and reopen it to trigger the checks, or merge it as an admin.

## When the sync fails

- **Merge conflict:** our change and Jellyfin's touch the same lines. Locally:

  ```sh
  git fetch upstream          # first time: git remote add upstream https://github.com/jellyfin/jellyfin-web.git
  git switch fluffy-moose && git pull
  git switch -c fluffy/sync-fix
  git merge upstream/release-12.z
  # fix the conflicted files, then
  git add -A && git commit
  ```

  Run the checks, push, and open a PR into `fluffy-moose`.
- **A check failed after a clean merge:** Jellyfin changed something our code
  relied on. Open the failed run, read the first error, and fix it the same way
  on a `fluffy/` branch.

## Moving to a new major version (e.g. 13)

1. Upgrade the server and the web client together, ideally on a quiet evening.
2. Merge `upstream/release-13.z` into `fluffy-moose` on a branch and fix any
   conflicts.
3. Change `UPSTREAM_BRANCH` at the top of `fluffy-upstream-sync.yml` to
   `release-13.z`.
4. Deploy the new build at the same time as you update the server image tag.
