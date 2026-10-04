---
type: atomic
tags: [devops, coding/quality, coding/distributed-systems]
date: 2026-10-04
---

# Silent Failure

## Idea
A silent failure is an error the system notices but nobody hears about. The job keeps "running", the log fills with the answer, and the damage piles up until someone stumbles on it.

## Definition
The usual cause is well-meant error handling: a `try/except` that catches an exception, prints it and carries on. The program survives, but the information goes nowhere a human looks. A scheduled job that wrote to an external service failed on every run for days; the log said exactly what was wrong the whole time, but nothing alerted, so it was found by accident. The fix is not to alert on every error, which trains people to ignore alerts, but to alert on **patterns** that need a human. **Streak-based alerting** works well for scheduled jobs: count consecutive failures, send one alert when the streak reaches a threshold (say three in a row), stay quiet while it continues, and send a recovery notice when it clears. Count streaks **per run and per destination**, so one broken integration is visible on its own instead of being averaged away by the healthy ones. A single transient blip never pages anyone; a persistent break always does, exactly once. Pair this with a heartbeat for jobs that might not run at all, because a job that never starts produces no errors to count.

## Tools
- **Prometheus Alertmanager** — the `for:` clause fires only after a condition holds for a duration.
- **Healthchecks.io / dead man's switch services** — alert when a scheduled job fails to check in.
- **Sentry** — groups repeated exceptions and notifies on new or regressing issues.

## Source
"Fail-silent" is an established failure mode in fault-tolerant computing literature. The alerting practice comes largely from Google's *Site Reliability Engineering* book (Beyer et al., O'Reilly, 2016), which says every page should be actionable and should signal real impact, not noise.

---

## Compass

**Roots** — *where this comes from*
It is the exact opposite of [[Fail Fast Fail Loudly]], and it often hides behind well-intended [[Graceful Degradation]] that degrades without telling anyone.

**Paths** — *where this leads*
Errors are only findable if they are emitted as [[Structured Logging]] that can be queried and counted, and a [[Health Probe]] or heartbeat catches the case where the job never ran at all.

**Neighbors** — *what lives nearby*
A per-destination [[Write Ledger]] makes the failing pair obvious, and [[Instrument the Hypothesis]] is the habit of deciding up front what signal would tell you something is wrong.

**Clash** — *what pushes against this*
Too many alerts cause the same outcome as none, because people mute the channel. Thresholds also delay the first alert, which is wrong for failures where even one occurrence is serious, such as a security check that [[Fail Closed|failed open]].
