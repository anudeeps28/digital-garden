---
type: atomic
tags: [coding/cicd, coding/git, coding/testing, devops]
date: 2026-09-16
---

# The Merge Is What Gets Tested

## Idea
Your branch built clean on your machine. CI doesn't build your branch — it builds your branch combined with everything that landed on main while you were working.

## Definition
Most CI systems validate the *merge result*, not the commit you pushed: they create an ephemeral merge of your branch with the current target branch and build that. So a green local build proves your changes are internally consistent, and says nothing about whether they're consistent with the world your code is about to enter. The classic failure is semantic rather than textual — someone else renamed a property, changed a signature, or tightened a rule; Git merges both changes without a conflict because the lines don't overlap, and the build breaks on code neither of you wrote wrong. The practical habit is to merge or rebase onto the target branch *before* pushing, so you see the real build. The general principle: local success is evidence about a state that isn't the one being shipped.

## Source
Behaviour of merge-commit validation in GitHub Actions (`pull_request` events build the merge ref), Azure DevOps PR builds, and GitLab merged-results pipelines.

---

## Compass

**Roots** — *where this comes from*
It follows from the way branches diverge in [[Git Branches]], and from semantic conflicts that textual merging cannot see.

**Paths** — *where this leads*
Shorter-lived branches shrink the divergence window, which is the actual structural fix; [[git pull --rebase vs git pull]] governs how you close it.

**Neighbors** — *what lives nearby*
[[Tier-Gated Features]] is the same category of error in the infrastructure world — local validation passing a thing the real target rejects.

**Clash** — *what pushes against this*
Constantly rebasing onto a fast-moving main is churn, and [[Never Rebase Already-Pushed Commits]] limits when you can. Sometimes the honest answer is to let CI find it.
