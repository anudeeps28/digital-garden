---
type: atomic
tags: [devops, coding/database, coding/azure, coding/distributed-systems]
date: 2026-09-16
---

# Geo-Redundant Backup

## Idea
A backup stored next to the thing it protects is not a backup. It's a second copy of the same single point of failure.

## Definition
Geo-redundant backup means backup copies are replicated to a physically separate region, so a regional outage, a datacentre fire, or a region-wide misconfiguration cannot destroy both the primary and its recovery path. Cloud platforms expose this as a redundancy setting — locally redundant (same datacentre), zone redundant (separate buildings in one region), geo-redundant (a paired region hundreds of miles away) — with cost rising accordingly. The sane default is to vary it by environment: geo-redundant in production, locally redundant everywhere else, because a dev environment's backup is not worth cross-region egress. Expressing that as one conditional in [[Infrastructure as Code]] rather than a manual setting per environment is what stops production quietly ending up on the cheap option.

## Source
Standard cloud storage redundancy tiers — Azure LRS/ZRS/GRS, AWS S3 cross-region replication, Google Cloud multi-region buckets.

---

## Compass

**Roots** — *where this comes from*
It follows from taking [[Fault-vs-Failure]] seriously at the level of a whole region, not just a process.

**Paths** — *where this leads*
Redundancy is only half the story — the other half is the [[Restore Drill]] that proves the copy is usable.

**Neighbors** — *what lives nearby*
[[Graceful Degradation]] keeps a system partially serving during failure; geo-redundancy is about surviving the failure of everything at once.

**Clash** — *what pushes against this*
Cross-region replication costs money and adds replication lag, so the recovery point is never exactly zero. Below production, the cost usually isn't justified — which is exactly why the setting must be deliberate rather than uniform.
