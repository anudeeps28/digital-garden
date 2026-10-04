---
type: atomic
tags: [devops, coding/git, coding/distributed-systems]
date: 2026-10-04
---

# Pull-Based Deployment

## Idea
Instead of a pipeline pushing code to the server, the server pulls the latest version of the repo on its own schedule.

## Definition
In push-based deployment, a [[CI-CD Pipeline]] holds credentials to the server and copies code onto it. In **pull-based** deployment the server holds read access to the repo and updates itself. The simplest form: the production box is a git clone, and a scheduled `git pull` runs an hour before the jobs that use the code, so every run uses the latest `main`. Nothing outside needs SSH keys to production, and the deploy mechanism is a single line. The subtle consequence is **overlap**: between one pull and the next, old and new code coexist with the same data. A job started on the old version may meet records written by the new one, or a pull may land mid-run. So jobs must be [[Idempotency|idempotent]] and data formats backward compatible across at least one version. The formal version of this idea is **GitOps**: the desired state lives in git, and an agent in the cluster continuously reconciles reality to match it, also correcting drift.

## Tools
- **Argo CD** and **Flux** — GitOps controllers for Kubernetes.
- **cron or launchd plus `git pull`** — the minimal single-server version.

## Source
GitOps was named by Alexis Richardson of Weaveworks in August 2017; Weaveworks built Flux, and Argo CD came from Intuit (2018). Both are CNCF projects.

---

## Compass

**Roots** — *where this comes from*
It treats [[Git]] as the [[Single Source of Truth]] for what should be running, and it is usually driven by [[Cron]] or [[launchd]].

**Paths** — *where this leads*
Overlapping versions demand [[Idempotency]] and careful [[Database Migrations]], and a stateless host makes it pair naturally with [[Docker Compose]].

**Neighbors** — *what lives nearby*
[[Branch-based Deployments]] decide which branch a server tracks, and [[Pre-deploy Approvals]] can still gate what gets merged into it.

**Clash** — *what pushes against this*
There is no immediate deploy or clear "deploy finished" signal, and a broken commit spreads silently on the next pull unless tests gate the branch, so [[The Merge Is What Gets Tested]] matters.
