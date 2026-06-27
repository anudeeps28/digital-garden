---
type: atomic
tags: [coding/devops, coding/cicd, coding/git]
date: 2026-04-24
---

# Branch-based Deployments

## Idea
A branching strategy where the branch a commit lives on determines which environment it deploys to — `master` → prod, `release/*` → test, feature branches → dev — making the branch name itself the deployment target.

## Definition
Branch-based deployment couples Git topology to the [[Release Stages|release pipeline]]: the [[CI-CD Pipeline]] watches multiple branches, builds [[Build Artifacts|artifacts]] from each, and uses [[Artifact Filters]] in the release pipeline to send artifacts to the right environment based on the source branch. KBA's pattern: feature branches build but don't auto-promote past Dev; `master` builds promote through Test → Prod (with approvals); `release/*` branches build for staging environments. The advantages: zero ambiguity about what's deploying where, easy mental model, and `git log master` is the production deploy history. The trap covered in [[Build Pipeline vs Release Pipeline]]: if you fix something on a feature branch and forget to merge, the fix never reaches the environments your watcher is filtering for. The pipeline doesn't lie — it just won't deploy code from branches it isn't watching.

## Source
CI/CD learning session — KBA's branch-to-environment mapping.

---

## Compass

**Neighbors** — *what lives nearby*

[[GitFlow]] is a full-blown branching strategy that codifies this pattern, while [[Trunk-based development]] is the lightweight cousin that uses one branch with environment-by-config instead. [[Environment branches (dev/test/prod branches)]] represent a heavier variant of the same idea.

**Clash** — *what pushes against this*

[[Tag-based deployments]] flip the model — promotion becomes "tag a commit" rather than "land on a branch" — and manual deploy from any commit eliminates branch policy entirely.

**Roots** — *where this comes from*

This pattern belongs to the broader domain of [[Git Branches]] and branching strategy, which is a foundational decision in any CI/CD setup. It exists to address the [[Release Stages]] problem — determining where a given artifact should go in the pipeline.

**Paths** — *where this leads*

Branch-based deployments are enforced by [[Artifact Filters]], the mechanism that actually maps branches to environments. This pattern also spawns variations like hotfix branch patterns for emergency fixes and [[Branch protection rules]] to prevent direct pushes to deploy branches.
