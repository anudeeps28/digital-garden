---
type: atomic
tags: [coding/git, workflow]
date: 2026-02-24
---

# Never Rebase Already-Pushed Commits

## Idea
Rebase is safe when your commits are local only — the moment someone else has pulled your commits, rebasing them breaks their history.

## Definition
Rebasing rewrites commits (same changes, new hashes). If you rebase commits that teammates have already based their work on, those teammates now reference commits that no longer exist on the remote. Their branches diverge and reconciling it is messy and confusing.

**The golden rule:** *Never rebase commits that have already been pushed to a shared branch.*

Before rebasing, ask: *"Has anyone else pulled my commits?"*
- No → rebase freely
- Yes → use merge instead

**Safe to rebase:**
- Local commits not yet pushed
- A feature branch you solely own (and you're comfortable force-pushing it)

**Never rebase:**
- `main`, `develop`, or any shared branch others are actively pulling from
- Any commits you've already pushed and shared

## Source
Git knowledge chat log — risks of rewriting history

---

## Roots — *where this comes from*
This principle comes from broader thinking about [[Optimize for Future Teammates Reading Your History]], because shared branch history needs to be stable so teammates can reliably track what's happened and build on top of it.

## Paths — *where this leads*
Understanding this principle unlocks safe use of [[git pull --rebase vs git pull]] on feature branches, and enables team trust where teammates can confidently rely on shared branch history being immutable and predictable.

## Neighbors — *what lives nearby*
The spirit mirrors [[Fail Fast Fail Loudly]] — the key is not creating hidden problems for others. Force-push is the only way to push after rebasing already-pushed commits, which itself carries significant risks.

## Clash — *what pushes against this*
The opposite perspective is to rebase everything freely, but this only works when you're operating entirely solo and have no teammates depending on the commits you push.
