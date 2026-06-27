---
type: atomic
tags: [coding/devops]
date: 2026-03-24
---

# Pull Request

## Idea
A pull request is a formal request to merge your branch into the main codebase, reviewed by teammates before approval.

## Definition
A Pull Request (PR) is a [[Git]] workflow mechanism where a developer says "my [[Git Branches|branch]] is ready — please review and merge it." The PR shows all the code changes (diffs), and teammates can comment, request changes, or approve. In [[Azure DevOps]], PRs can have required reviewers, linked work items, and automated checks (like the [[CI-CD Pipeline]] running [[Unit Tests]]). PRs are a quality gate — they catch bugs, enforce standards, and share knowledge across the team. In the project, every code change goes through a PR before reaching the main branch.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Code Review]] is the practice of reviewing code that PRs formalize and enforce. [[Merge Request]] is GitLab's equivalent term for the same workflow.

**Clash** — *what pushes against this*
[[Direct Push to Main]] bypasses review altogether by pushing code straight to main, while [[Pair Programming]] achieves code review in real-time rather than asynchronously through a formal PR process.

**Roots** — *where this comes from*
PRs build on the concept of [[Git Branches]], which they merge into main, and modern platforms like [[Azure DevOps]] provide the infrastructure to host PRs with policies and automated checking.

**Paths** — *where this leads*
When a PR merges, it triggers the [[CI-CD Pipeline]] to automatically run deployment pipelines, and the merge becomes part of the [[Git]] history as a merge commit.
