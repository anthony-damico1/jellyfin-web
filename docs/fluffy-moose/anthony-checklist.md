# First-time setup checklist (for Anthony)

Only the repo owner can do these, and you only do them once. Each step is a
few clicks on github.com. Tick them off in order.

## 1. Check Actions is on (the robot that tests our changes)

- [ ] Open the repo on GitHub and click the **Actions** tab at the top.
- [ ] If you see runs listed, it's already on, so move to step 2. If you see a
  green **"I understand my workflows, go ahead and enable them"** button,
  click it.

## 2. Let the robot open pull requests

- [ ] Click **Settings** (top right of the repo, the gear icon).
- [ ] In the left menu, click **Actions**, then **General**.
- [ ] Scroll to **Workflow permissions**.
- [ ] Choose **Read and write permissions**.
- [ ] Tick **Allow GitHub Actions to create and approve pull requests**.
- [ ] Click **Save**.

## 3. Merge the first pull request

- [ ] Click the **Pull requests** tab and open the one called *"Fork docs, PR checks and weekly upstream sync"*.
- [ ] Read it. **Files changed** shows exactly what's new.
- [ ] Wait for the checks at the bottom to go green ✅ (about 5 minutes).
- [ ] Click **Merge pull request**, then **Confirm merge**.

## 4. Make `fluffy-moose` the main branch

GitHub currently opens on `master`, which is Jellyfin's unreleased code and
doesn't match our server. The weekly update check also only runs from the
main branch.

- [ ] **Settings** → **General** → **Default branch**.
- [ ] Click the ⇄ (two arrows) button, pick **fluffy-moose**, click **Update**,
  then confirm.

## 5. Stop anyone pushing straight to `fluffy-moose`

This makes every change go through a pull request, so the tests run first.

- [ ] **Settings** → **Branches** → **Add classic branch protection rule**.
- [ ] Branch name pattern: `fluffy-moose`
- [ ] Tick **Require a pull request before merging**. Untick **Require
  approvals** for now. With only two of us, approvals would block us.
- [ ] Click **Create**.

## 6. Get emails when something needs you

- [ ] On the repo's front page, click **Watch** (top right) → **All Activity**.

You'll now get an email when the weekly Jellyfin update PR opens, or when an
automatic check fails.

## 7. Tell Cian two things about the server

Run this on the server and send the output to Cian:

```sh
docker ps --format '{{.Names}}  {{.Image}}'
```

That shows which Jellyfin image we're on, and whether something like
Watchtower updates it automatically.

## 8. (Optional) Try the update check once by hand

- [ ] **Actions** tab → **Upstream sync** (left list). If it says the workflow
  is disabled, click **Enable workflow**.
- [ ] Click **Run workflow** → **Run workflow**.
- [ ] Wait for it to finish. A green ✅ with "already up to date" is the normal result today.

---

That's it. After this, day to day you just open the **Pull requests** tab,
look at what's there, and press **Merge** when the checks are green.
