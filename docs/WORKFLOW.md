# My GitHub workflow

A short guide to how every repo on this account works, and what to do when things go wrong.

## The loop: branch → PR → CI → auto-merge

```text
main ──┬────────────────────────────── squash merge ──▶ main
       └─ feat/my-change ── PR ── CI ✓ ──┘
```

1. **Start from an up-to-date `main`.**

   ```bash
   git switch main && git pull
   git switch -c feat/short-description     # or fix/…, docs/…, chore/…
   ```

2. **Commit small, one concern per commit.**

   ```bash
   git add -p                 # review hunks one by one, so you don't commit junk
   git commit -m "feat: add CSV export"
   ```

3. **Push and open a PR.**

   ```bash
   git push -u origin HEAD
   gh pr create --fill        # fill in the PR template, especially "What did I learn?"
   ```

4. **Turn on auto-merge** so it merges by itself once CI is green:

   ```bash
   gh pr merge --auto --squash
   ```

5. **CI runs.** `main` is protected, so the PR can only merge when:
   - the required checks (e.g. `web / test`, `backend / test`) pass,
   - the branch is up to date with `main`,
   - all review conversations are resolved.
6. **Squash merge.** The PR title becomes the single commit on `main`, and the branch is deleted.

### Why these rules?

| Rule | Why |
|---|---|
| No direct pushes to `main` | Every change gets CI, even "tiny" ones |
| 0 required approvals | I'm solo; requiring approval would block me |
| Required status checks | Broken code can't reach `main` |
| Branch must be up to date | Tests ran against what `main` will actually look like |
| Squash-only merges | One clean commit per PR, easy to revert |
| No force push / deletion on `main` | History can't be rewritten by accident |

### Dependabot

Dependabot opens weekly PRs for npm / pip / GitHub Actions updates.
**Patch and minor** updates auto-merge once CI passes. **Major** updates wait for me,
because they can include breaking changes: read the changelog, then merge.

---

## Resolving merge conflicts

A conflict means `main` and your branch both changed the same lines, and git can't decide
which version wins. You decide.

### Option 1: rebase on the command line (recommended)

```bash
git fetch origin
git rebase origin/main
```

Git stops at each conflicting commit. Open the file and you'll see:

```text
<<<<<<< HEAD (origin/main, what's already merged)
const limit = 10;
=======
const limit = 25;
>>>>>>> feat/my-change (your commit)
```

Edit it to the correct final version (keep one side, the other, or combine them), delete
the markers, then:

```bash
git add path/to/file
git rebase --continue       # repeat until done
# changed your mind?  git rebase --abort  puts everything back
npm test / pytest           # make sure the combined result still works
git push --force-with-lease # safe force push: only updates YOUR branch, and refuses
                            # if someone else pushed to it since you last fetched
```

> Never force push to `main`. The ruleset blocks it anyway.

### Option 2: GitHub's "Resolve conflicts" button

On the PR page, click **Resolve conflicts**. It opens a web editor with the same
`<<<<<<< / ======= / >>>>>>>` markers. Fix each file, click **Mark as resolved**, then
**Commit merge**. Good for small text conflicts. This creates a merge commit on your
branch, which is fine because the PR is squashed anyway.

### Option 3: VS Code merge editor

After `git rebase origin/main` stops on a conflict, open the file in VS Code and click
**Resolve in Merge Editor**. You get three panes: *Incoming* (`main`), *Current*
(your change) and *Result*. Tick the changes to keep, edit the result, then
**Complete Merge** and run `git rebase --continue`.

### Option 4: ask an AI to explain both sides

When you don't understand why the other side changed something:

- **Copilot Chat** (VS Code): select the conflict block and ask
  *"Explain what each side of this conflict is trying to do, and propose a merged version that keeps both intents."*
- **Claude Code**: run `claude` in the repo while the rebase is paused and ask
  *"Explain the conflict in `path/to/file`: what did main change, what did my branch change, and what's the correct combination? Don't continue the rebase, just show me."*

Always read the proposed result and run the tests. The AI doesn't know which behaviour
you actually want.

### Avoiding conflicts in the first place

- Keep branches short-lived (hours to days, not weeks).
- `git fetch && git rebase origin/main` before you open the PR.
- Don't mix formatting-only changes with real changes in the same PR.
