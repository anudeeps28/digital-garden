---
type: atomic
tags: [devops, coding/devops, coding/cicd]
date: 2026-10-01
---

# DevOps Platform

## Idea
A DevOps platform puts the code, the to-do list and the deployment machinery in one product, so you can follow a single change from "someone asked for this" to "it is running in production" without jumping between tools.

## Definition
A DevOps platform is one product that bundles the main tools a software team uses: **repositories** hosting [[Git]] code, **work tracking** (boards of tasks and bugs, often in a [[Kanban]] style), **[[CI-CD Pipeline|CI/CD pipelines]]** that build, test and deploy, **artifact feeds** that store packages and [[Build Artifacts]], and often **test plans** for manual testing. The value is in the links between them. A commit message that mentions a work item number attaches the commit to that item; opening a [[Pull Request]] automatically runs a pipeline and blocks merging until it passes; a deployment through [[Release Stages]] shows which work items it shipped. That gives you **traceability**: for any production change you can answer who asked for it, who reviewed it and when it went out. Pipelines run on [[Pipeline Agent Machines]], either hosted by the vendor or self-hosted inside your network. The trade-off is integration versus lock-in. Everything works together with little glue, but pipeline definitions, permissions, branch policies and history are written in that vendor's format, so moving to another platform means rewriting pipelines and migrating years of linked records, which rarely transfers cleanly.

## Providers
- **Azure** — Azure DevOps: Repos, Boards, Pipelines, Artifacts and Test Plans as separate services in one organization.
- **AWS** — AWS CodeCatalyst bundles repos, issues and workflows; the older CodeCommit, CodeBuild and CodePipeline are separate pieces.
- **Google Cloud** — no single bundle; Cloud Build and Artifact Registry are usually paired with GitHub or GitLab.
- **Others** — GitHub (repos plus Actions, Projects and Packages); GitLab (a single application covering the whole lifecycle); Atlassian (Bitbucket for code, Jira for work, Bamboo or Bitbucket Pipelines for CI/CD).

## Source
The term grew out of the DevOps movement (around 2009); Microsoft's Team Foundation Server (2005, renamed Azure DevOps in 2018) and GitLab were early all-in-one examples.

---

## Compass

**Roots** — *where this comes from*
It grew from [[Git]] hosting plus a [[CI-CD Pipeline]], with work tracking added so code and requests live together.

**Paths** — *where this leads*
Once pipelines run there, it becomes the place for [[Release Stages]], [[Pre-deploy Approvals]] and [[Build Pipeline vs Release Pipeline|build/release separation]].

**Neighbors** — *what lives nearby*
[[Pull Request]] policies and [[Git Branches]] rules are enforced by the platform, and [[Pipeline Agent Machines]] do the actual work.

**Clash** — *what pushes against this*
Best-of-breed teams argue that one vendor's average tool in each category is worse than the best tool in each, and the deep links that make the platform useful are exactly what makes leaving it expensive.
