---
type: atomic
tags: [coding/devops, coding/cicd]
date: 2026-04-24
---

# Artifact Filters

## Idea
Artifact filters are conditions on a release stage that decide whether a given build is allowed to deploy here — most commonly "only artifacts built from `master`" — a deliberate safety, not a bug.

## Definition
In Azure DevOps Classic Releases, each stage's "pre-deployment conditions" can include an **artifact filter**: a rule that inspects the [[Build Artifacts|artifact]]'s metadata (source branch, build tags, build number) and either allows or skips the deployment. The most common filter is `sourceBranch: master` on the Test and Prod stages — meaning only builds produced from `master` will trigger those stages. A build from a feature branch will reach the artifact store, may even auto-deploy to Dev, but the Test stage will silently skip it. **This is a feature, not a bug** — it prevents random feature-branch builds from sneaking into Test or Prod. The trap: if you don't know the filter exists, the symptom looks like "the pipeline is broken" — your build succeeded, so where's my deploy? Always check the artifact filter before assuming a stage is misconfigured.

## Source
CI/CD learning session — Franco's deliberate `sourceBranch: master` filter that initially looked like a bug.

---

## Compass

**Roots** — *where this comes from*
Filters guard the boundary between [[Release Stages]], acting as the infrastructure that enforces "working as designed" versus flagging what's actually broken.

**Paths** — *where this leads*
Artifact filters implement the broader pattern of [[Branch-based Deployments]], but sometimes you need to bypass the filter for hotfix branches, which raises questions about the audit trail — who relaxed a filter and why.

**Neighbors** — *what lives nearby*
[[Pre-deploy Approvals]] serve a similar role as another kind of stage gate, and branch protection rules on the source-control side are the analogous concept, as are webhook filters which apply the same filtering idea to event triggers.

**Clash** — *what pushes against this*
The opposite extreme is a "deploy any artifact" approach with no filter at all — every build gets promoted — or switching to manual-only triggers where explicit human action replaces the filtering mechanism entirely.
