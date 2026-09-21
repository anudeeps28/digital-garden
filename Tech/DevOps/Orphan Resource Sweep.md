---
type: atomic
tags: [devops, iac, coding/quality, coding/cicd]
date: 2026-09-16
---

# Orphan Resource Sweep

## Idea
The bugs you find by reading code are the ones you thought to look for. The bugs you find by crossing two lists against each other are the ones nobody thought about at all.

## Definition
An orphan resource sweep is a systematic cross-check of two inventories that should correspond exactly, looking for entries present in one and absent from the other. Concretely: list every application in the solution, list every host defined in the infrastructure templates, list every entry in the deployment pipeline — then take the set differences. Applications with nowhere to run are orphans; hosts with nothing to run on them are waste; pipeline stages pointing at either are broken. It works because the failure it catches is an *absence*, and absences are invisible when you read either list on its own — nothing looks wrong in a file that's simply missing an entry. The same mechanical check finds a value written in two places that has drifted apart in one: enumerate, compare, don't reason.

## Source
A general auditing technique; appears as reconciliation in accounting and as drift detection in [[Infrastructure as Code]] tooling (`terraform plan`, Azure what-if).

---

## Compass

**Roots** — *where this comes from*
It's only possible once the environment is declared in files — a [[Infrastructure as Code]] dividend, because you can't diff a portal.

**Paths** — *where this leads*
Once run by hand, the sweep is worth automating as a CI check, since orphans reappear every time someone adds a component.

**Neighbors** — *what lives nearby*
[[Single Source of Truth]] is the preventive version — remove the second list so there's nothing to diverge.

**Clash** — *what pushes against this*
Cross-checking is tedious and produces nothing on most runs, which makes it the first check to be skipped and the one that silently rots once automated.
