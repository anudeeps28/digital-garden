---
type: atomic
tags: [coding/git, workflow]
date: 2026-02-24
---

# git pull --rebase vs git pull

## Idea
`git pull --rebase` rewrites your local commits on top of remote changes for a clean linear history; `git pull` creates a merge commit that honestly records two histories joining.

## Definition
Both sync your branch with the remote, but they differ in *how* they join the histories:

- **`git pull` (merge)** — fetches remote changes and creates a merge commit `M`. Preserves the true history of when two parallel lines of work were combined. Can clutter the log with many merge commits over time.
- **`git pull --rebase`** — fetches remote changes, temporarily removes your local unpushed commits, fast-forwards to the remote, then replays your commits on top as new commits (`C` becomes `C'`). No merge commit. Clean, linear history.

*Mental model: merge says "these two histories joined here." Rebase says "pretend I always started from the latest code."*

**When to use which:**
- Feature branches you own → `git pull --rebase`
- Shared integration branches (`main`, `develop`) → `git pull` (merge), or better, never pull directly — use PRs

**Recommended daily habit (founding engineer / solo on many branches):**
```bash
git fetch --all       # see everything that changed remotely first
git status            # check where you are
git pull --rebase     # then sync your current branch
```

Set as global default: `git config --global pull.rebase true`

## Source
Git knowledge chat log — pull vs rebase mechanics, visual walkthrough

---

## Compass

**Neighbors** — *what lives nearby*
`git fetch` + `git merge` is what `git pull` does under the hood, and [[git rebase (interactive)]] offers the same concept with more control over how you reshape your history.

**Clash** — *what pushes against this*
Merge commits are honest but can make history noisy as they accumulate, while blindly running `git pull` without checking your state first can lead to unexpected merge commits and tangled history.

**Roots** — *where this comes from*
This connects to [[Optimize for Future Teammates Reading Your History]], a broader theme about how you keep a git history readable as a team grows and more people touch the codebase.

**Paths** — *where this leads*
The key safety rule that makes rebase safe is [[Never Rebase Already-Pushed Commits]], and using rebase leads to cleaner `git log`, easier `git bisect`, and more readable code reviews overall.
