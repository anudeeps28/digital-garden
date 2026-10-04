---
type: atomic
tags: [devops, coding/distributed-systems, coding/database]
date: 2026-10-04
---

# RTO and RPO

## Idea
Two numbers define a backup strategy: how long you can be down (RTO) and how much recent data you can afford to lose (RPO).

## Definition
The **Recovery Time Objective** is the maximum acceptable time from an outage to service being restored. The **Recovery Point Objective** is the maximum acceptable data loss, measured as time: how far back the newest usable backup may be. They are set by the business, then the architecture has to meet them. A small worked example: target RTO under 30 minutes and RPO under 24 hours. A nightly database dump meets the RPO (worst case you lose a day), while point-in-time recovery from the managed database brings RPO close to zero for the same data. A stateless host rebuilt from git with one command meets the RTO. Writing the numbers down also forces honest decisions about what *not* to back up: generated images that can be recreated from their inputs were judged not worth backing up because they are replaceable. The numbers mean nothing until tested; only a timed restore tells you your real RTO.

## Source
Standard business-continuity vocabulary that grew out of 1970s-80s mainframe disaster recovery planning; formally defined in ISO 22301 and its vocabulary standard ISO 22300. A single originator could not be verified.

---

## Compass

**Roots** — *where this comes from*
It comes from disaster recovery planning and connects to [[Fault-vs-Failure]], since both ask what happens after something breaks rather than whether it will.

**Paths** — *where this leads*
The only proof you meet the numbers is a [[Restore Drill]], and a tighter RPO usually means [[Geo-Redundant Backup]] or point-in-time recovery.

**Neighbors** — *what lives nearby*
[[Stateless Services]] and [[Docker Compose]] make RTO small, because a host can be rebuilt rather than repaired. [[Blast Radius]] asks the related question of how much breaks at once.

**Clash** — *what pushes against this*
Near-zero RTO and RPO cost real money in replicas and standby capacity, and for a small app the honest answer is often to accept a day's loss. Untested targets give false confidence, which is a quiet [[Silent Failure]].
