---
type: atomic
tags: [coding/devops]
date: 2026-03-24
---

# Git

## Idea
Git is a version control system that tracks every change to every file — allowing you to collaborate, review history, and undo mistakes.

## Definition
Git is a distributed version control system that records a complete history of every change made to your codebase. Each change is captured in a commit (a snapshot with a message explaining what changed and why). Git enables parallel development through [[Git Branches|branches]], collaboration through [[Pull Request|pull requests]], and safety through the ability to revert any change. In practice, teams host code in Git repositories, work on feature branches, submit PRs for code review, and merge into the main branch, which typically triggers automated processes like [[CI-CD Pipeline|CI/CD pipelines]].

## Source
Linus Torvalds, created in 2005 to manage the Linux kernel development. Introduced as a distributed version control system with speed, data integrity, and non-linear workflow support.

---

## Compass

**Neighbors** — *what lives nearby*
[[SVN]] is an older centralized version control system that served a similar purpose, and [[Mercurial]] is another distributed version control system like Git.

**Clash** — *what pushes against this*
[[No Version Control]] — where developers edit files directly on a shared drive — represents the complete absence of systematic change tracking. [[Manual Backups]], copying folders to track versions, is a primitive precursor that lacks Git's structured history and collaboration.

**Roots** — *where this comes from*
Git is foundational to [[DevOps]], enabling modern DevOps practices and serving as the backbone for version control in contemporary software development.

**Paths** — *where this leads*
Git enables [[Git Branches]] for parallel development streams and [[Pull Request|pull requests]] for structured code review workflows. Git pushes trigger automated processes like the [[CI-CD Pipeline]], and changes to the database are tracked through [[Database Migrations]] in the repository.
