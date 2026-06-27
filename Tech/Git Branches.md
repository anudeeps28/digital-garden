---
type: atomic
tags: [coding/devops]
date: 2026-03-24
---

# Git Branches

## Idea
Branches are separate copies of the code where you work on features without breaking the main codebase.

## Definition
A [[Git]] branch is a lightweight pointer to a series of commits that diverges from the main line of development. When you create a branch (e.g., `feature/add-upload-endpoint`), you get your own workspace where you can make changes without affecting `main`. Other developers can work on their own branches simultaneously. When your feature is ready, you create a [[Pull Request]] to merge your branch back into main. In the KBA project, the team follows a branch-per-feature workflow: each story or bug fix gets its own branch, is reviewed via PR, and then merged.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Git Forks]] provide a copy of the entire repository common in open-source contexts, while [[Feature Flags]] offer another way to develop features in parallel without needing separate branches.

**Clash** — *what pushes against this*
[[Trunk-Based Development]] takes the opposite approach by having everyone commit directly to main with no long-lived branches, and [[Working Directly on Main]] abandons branching entirely, making changes without isolation—a risky practice.

**Roots** — *where this comes from*
Branches are a core feature of [[Git]] itself, and in enterprise contexts like [[Azure DevOps]], branch policies enforce code review rules to maintain quality standards.

**Paths** — *where this leads*
Branches flow into [[Pull Request|Pull Requests]], which are the mechanism for merging your work back into main, and they integrate with [[CI-CD Pipeline|CI-CD pipelines]] that automatically build and validate code before merging occurs.
