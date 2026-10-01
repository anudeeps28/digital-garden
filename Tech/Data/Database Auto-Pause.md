---
type: atomic
tags: [coding/database, coding/azure, devops]
date: 2026-10-01
---

# Database Auto-Pause

## Idea
Auto-pause lets a database switch its compute off when nobody is using it, so an idle database costs only its storage. The price is that whoever connects first has to wait for it to wake up.

## Definition
Auto-pause is a feature of serverless database tiers. After the database has had no activity for a set **auto-pause delay**, the provider releases its compute and stops billing for it; you keep paying for storage. The next connection attempt triggers an automatic **resume**, which brings compute back and lets the connection through. The catch is that resume isn't instant. It can take tens of seconds, sometimes about a minute, and during that time the first connection either waits or fails. To an app without retry logic this looks exactly like a timeout or a database outage: a request errors, someone refreshes, and now it works. So the database needs [[Connection Resiliency]] in front of it: connection timeouts long enough to cover a resume, plus retries with [[Exponential Backoff|backoff]]. Background activity can also keep it awake without you noticing (health checks, monitoring queries, a scheduled job), so you never see the savings. That makes auto-pause a good fit for dev, test and demo databases that sit idle overnight, and a risky one for production, where the first user after a quiet period gets the slow or failing request.

## Providers
- **Azure** — Azure SQL Database serverless (General Purpose tier) with a configurable auto-pause delay.
- **AWS** — Aurora Serverless v2, which can scale down to 0 ACUs (capacity units) and pause when idle.
- **Google Cloud** — no direct equivalent for Cloud SQL; instances can be stopped manually or on a schedule.
- **Others** — Neon's scale-to-zero for serverless PostgreSQL, which suspends compute after a few idle minutes.

## Source
Azure SQL Database serverless (Microsoft, 2019) made auto-pause common for relational databases; Aurora Serverless v2 added scaling to zero in 2024.

---

## Compass

**Roots** — *where this comes from*
It's [[Scale-to-Zero]] applied to the database tier of a [[Managed SQL Database]].

**Paths** — *where this leads*
Turning it on means building [[Connection Resiliency]] into every client, and deciding which environments can live with a cold first request.

**Neighbors** — *what lives nearby*
[[Exponential Backoff]] is the retry pattern that hides a resume from users; [[Graceful Degradation]] covers what a user sees while the database wakes.

**Clash** — *what pushes against this*
The savings are real only if the database is truly idle for long stretches. For anything a user waits on, a slow or failed first request usually costs more than the compute it saved.
