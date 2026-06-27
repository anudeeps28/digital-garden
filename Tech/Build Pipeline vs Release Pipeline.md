---
type: atomic
tags: [coding, devops, cicd, deployment]
date: 2026-04-02
---

# Build Pipeline vs Release Pipeline

## Idea
The build pipeline compiles your code into an artifact; the release pipeline takes that artifact and deploys it to environments — two separate stages.

## Definition
In [[Azure DevOps]] (and most CI/CD systems), deployment is split into two stages:

**Build Pipeline** (CI — Continuous Integration):
- Triggered by code commits (usually to specific branches like `master`, `release/*`)
- Compiles the code, runs tests, produces a **build artifact** (a zip/package of your compiled app)
- Defined in `azure-pipeline.yml` in your repo
- Output: a versioned artifact stored in Azure DevOps

**Release Pipeline** (CD — Continuous Deployment):
- Takes a build artifact and **deploys** it to one or more environments (dev → test → prod)
- Can be triggered automatically (after build completes) or manually
- Can include extra steps: [[Migration Scripts (DBAUp)]], health checks, approval gates
- Configured in Azure DevOps Releases (not in code)

**Why the separation matters:**
- You build **once**, deploy **many times** — same artifact goes to dev, test, prod
- Build and release can be triggered independently — you can re-deploy an old build without rebuilding
- Different people can have permissions for build vs release (devs can build, only ops can release to prod)

**In PlanDocumentRAG:**
- Build pipeline only triggers on `master` and `release/*` branches — the `fix/iis-deployment-fixes` branch couldn't be built by the pipeline
- Release pipeline includes a DBAUp task for database migrations
- Franco could trigger a release manually from Azure DevOps

**Key lesson:** If your code is on a feature branch that the build pipeline doesn't watch, your fixes will never get deployed — no matter how many times you push. Either merge to master or manually adjust the pipeline trigger.

## Source
PlanDocumentRAG deployment — CORS fixes were stuck on an unmerged branch. Pipeline only built master. This caused hours of "why isn't it working?" because the deployed code never had the fixes.

---

## Compass

**Neighbors** — *what lives nearby*
The [[CI-CD Pipeline]] is the combined concept that encompasses both build and release stages. [[Docker Image]] is another form of build artifact that can be versioned and deployed across environments. [[Git Branches]] determine what gets built, so your branch strategy directly influences what the pipeline will process.

**Clash** — *what pushes against this*
Manual deployment — copying files to server by hand with no pipeline — represents the opposite approach. The "Works on my machine" problem arises when there's no standardized build/deploy process, defeating the entire purpose of separation.

**Roots** — *where this comes from*
This concept lives within [[Azure DevOps]], where The project's pipelines are hosted and managed. It's an implementation of the broader [[CI-CD Pipeline]] pattern that separates concerns between building code and deploying it.

**Paths** — *where this leads*
[[Migration Scripts (DBAUp)]] often run as part of the release pipeline to handle database changes. The principle of "build once, deploy everywhere" connects to [[Runtime Config (Build Once Deploy Everywhere)]], where one build artifact is deployed with different configurations per environment. Understanding this separation informs critical branch strategy decisions — which branches should trigger builds?
