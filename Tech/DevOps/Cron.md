---
type: atomic
tags: [devops, workflow]
date: 2026-10-04
---

# Cron

## Idea
Cron runs commands on a schedule written as five time fields, and its simplicity hides two classic traps: everyone runs on the hour, and chained jobs fail silently.

## Definition
A crontab line has five fields, **minute hour day-of-month month day-of-week**, then the command: `7 21 * * *` means 21:07 every day. The daemon checks once a minute and runs whatever matches. Two lessons from real use. First, **avoid round times**. A nightly job scheduled at exactly 21:00 failed most nights with 502 and 503 errors from a CDN-fronted API, because huge numbers of other jobs worldwide also fire on the hour and congest the origin. Moving it to :07 and adding retries with backoff fixed it. Second, **do not chain unrelated jobs with `&&`**. Two jobs written as `job_a && job_b` meant every failure of the first silently skipped the second, and nobody noticed for weeks. Give each job its own line, its own log and its own alert. Also remember cron runs with a minimal environment (short `PATH`, no shell profile) and in the server's time zone, and that it simply skips runs while the machine is off.

## Source
Cron first appeared in Version 7 Unix (1979), written by Ken Thompson; Paul Vixie's rewrite (Vixie cron, 1987) is the basis of most Linux crons today. The syntax is standardised in POSIX.

---

## Compass

**Roots** — *where this comes from*
It is the original Unix scheduler and the default way to run batch work on any always-on server.

**Paths** — *where this leads*
Firing on the hour creates a [[Thundering Herd]], so schedules should be offset and paired with [[Exponential Backoff]]. Jobs that may re-run need [[Idempotency]].

**Neighbors** — *what lives nearby*
[[launchd]] is the macOS replacement that catches up on missed runs, and [[Structured Logging]] per job is what makes failures visible.

**Clash** — *what pushes against this*
Cron reports failure only by local mail no one reads, which makes it a factory for [[Silent Failure]]. Laptops that sleep miss runs entirely.
