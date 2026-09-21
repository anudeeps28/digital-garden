---
type: atomic
tags: [coding/git, workflow, productivity]
date: 2026-09-16
---

# Git Worktree per Task

## Idea
Switching branches in one directory means stashing, rebuilding, and losing your place. A worktree gives each task its own directory off the same repository, so switching tasks is switching windows.

## Definition
`git worktree add` creates an additional working directory attached to an existing repository, checked out to its own branch, sharing the same object store and history. Each worktree keeps its own working tree, index, and — critically — its own build output, so moving between two pieces of work costs nothing: no stash, no recompile, no half-applied state. It suits a rhythm of one isolated unit of work per directory: branch, build, test, review, open the pull request, remove the worktree. The constraints are that two worktrees can't have the same branch checked out, and that anything living outside version control — local settings, environment files, dependency caches — doesn't come along and has to be provisioned per worktree.

## Source
Introduced in Git 2.5 (2015).

---

## Compass

**Roots** — *where this comes from*
It presupposes the short-lived-branch model of [[Git Branches]] — one unit of work, one branch, one review.

**Paths** — *where this leads*
Isolated directories make it practical to run a full build and test pass per task before opening a [[Pull Request]], and to keep several reviews in flight at once.

**Neighbors** — *what lives nearby*
It's the version-control expression of [[Environment Design]] — arrange the workspace so the right behaviour is the path of least resistance.

**Clash** — *what pushes against this*
Parallel tasks mean parallel divergence from main, which makes [[The Merge Is What Gets Tested]] bite harder. And each worktree is another full build directory on disk.
