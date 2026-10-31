---
type: atomic
tags: [coding/devops, careers]
date: 2026-10-31
---

# DevOps

## Idea
DevOps began as a culture idea: the people who write the code and the people who run it should work as one team. It grew into the name for a whole field of shipping and running software.

## Definition
Before DevOps, developers "threw code over the wall" to an operations team that deployed and ran it. Developers were rewarded for change, ops for stability, so the two sides fought. DevOps closes that gap with shared ownership and automation: [[CI-CD Pipeline|CI/CD]], [[Infrastructure as Code]], containers, monitoring and blameless [[Postmortem|postmortems]]. Several overlapping labels now share the same core skills:
- **DevOps** — the practice and, now, a job title covering pipelines, deployments and environments.
- **Cloud engineering** — designing and running systems on Azure, AWS or GCP; leans toward cloud services and architecture.
- **Site Reliability Engineering (SRE)** — Google's take: treat operations as a software problem, manage reliability with SLOs and error budgets, and cap manual "toil".
- **Platform engineering** — build internal tools and "paved roads" so product developers can ship without becoming infrastructure experts.
- **Infrastructure engineering** — the umbrella term for building the base everything runs on.

You don't need to pick a label to start; Linux, networking, containers, IaC and monitoring underpin all of them.

## Source
Patrick Debois coined the term with the first DevOpsDays in Ghent (October 2009). The talk most often cited as the spark is John Allspaw and Paul Hammond's "10+ Deploys Per Day: Dev and Ops Cooperation at Flickr" (Velocity, June 2009). SRE was started at Google by Ben Treynor Sloss in 2003. Platform engineering took its shape from *Team Topologies* (Skelton and Pais, 2019).

---

## Compass

**Roots** — *where this comes from*
It applies agile's short feedback loops to operations, and [[Separation of Duties]] is the older wall it set out to soften.

**Paths** — *where this leads*
Its everyday tools are the [[CI-CD Pipeline]], [[Docker]] and [[Infrastructure as Code]], usually hosted on a [[DevOps Platform]]. Its habits are [[Structured Logging]] and blameless [[Postmortem|postmortems]].

**Neighbors** — *what lives nearby*
[[Kaizen]] is the same small-continuous-improvement loop applied to manufacturing, and the [[The Flywheel Concept|flywheel]] describes how faster deploys produce faster feedback, which produces better deploys.

**Clash** — *what pushes against this*
Renaming the ops team "DevOps" without sharing ownership changes nothing, which is [[Goodhart's Law]] in job-title form. Regulated environments also keep some separation between whoever writes a change and whoever approves it on purpose, through [[Pre-deploy Approvals]].
