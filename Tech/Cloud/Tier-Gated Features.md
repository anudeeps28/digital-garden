---
type: atomic
tags: [coding/azure, iac, devops, coding/cicd]
date: 2026-09-16
---

# Tier-Gated Features

## Idea
Cloud providers put capabilities behind pricing tiers, and the type system doesn't know that. Your template compiles perfectly and the platform rejects it on the first real deploy.

## Definition
Tier-gated features are capabilities available only on a higher SKU of a cloud service — managed WAF rule sets on a premium edge tier, private endpoints on a premium messaging tier, geo-replication above a certain database tier. The hazard is specific to [[Infrastructure as Code]]: the template language validates *syntax and schema*, not *entitlement*. Requesting a premium-only feature on a standard SKU is structurally valid, so it type-checks, lints clean, and compiles — and is refused by the resource provider at deployment. The fix is to make tier and feature a single conditional decided together (premium SKU plus the ruleset in production, standard SKU without it below), so the two can never be set inconsistently. The broader lesson is that a green build is not evidence of a valid deployment; the only authority on what the platform accepts is the platform.

## Source
A recurring constraint across cloud SKU matrices — Azure Front Door Standard vs Premium, Azure SQL service tiers, AWS instance-class-gated features.

---

## Compass

**Roots** — *where this comes from*
The gap exists because [[Infrastructure as Code]] validation runs locally while entitlement is enforced remotely.

**Paths** — *where this leads*
It argues for a plan or what-if step against the real subscription before merge, and for keeping tier and dependent settings in one conditional rather than two.

**Neighbors** — *what lives nearby*
[[The Merge Is What Gets Tested]] is the same shape of error from a different direction — local success proving less than it appears to.

**Clash** — *what pushes against this*
The clean response is "just use the premium tier everywhere", which is correct and often costs several hundred dollars a month per environment. It's a budget decision wearing a technical costume.
