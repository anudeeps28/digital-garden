---
type: atomic
tags: [devops, workflow]
date: 2026-10-04
---

# launchd

## Idea
launchd is macOS's service manager and scheduler, and unlike cron it runs jobs that were missed while the Mac was asleep.

## Definition
launchd is the first process macOS starts, and it manages every daemon and agent on the system. You define a job with a **property list** (an XML `.plist`) that names a label, the program and arguments, and when to run it: `RunAtLoad` (at login), `StartInterval` (every N seconds), `StartCalendarInterval` (at specific times, cron-style) or on events like a file path changing. Per-user jobs live in `~/Library/LaunchAgents` and are loaded with `launchctl`. The key behavioural difference from cron: if a calendar-scheduled job's time passes while the machine is asleep, launchd runs it **once on wake** instead of skipping it. That makes it the right tool for a laptop that pulls data from an always-on server: the job catches up whenever the lid opens. It also sets stdout and stderr paths per job, so every run leaves a log. The rough edges are verbose XML, a minimal environment (set `PATH` explicitly) and missed runs while the machine is fully powered off.

## Source
Written by Dave Zarzycki at Apple and first shipped in Mac OS X 10.4 Tiger (2005), replacing init, cron, inetd and others on macOS.

---

## Compass

**Roots** — *where this comes from*
It replaces [[Cron]] on macOS and folds scheduling into service management, the same role systemd later took on Linux.

**Paths** — *where this leads*
Because a missed run fires late on wake, jobs should be safe to run at any time and more than once, which is [[Idempotency]].

**Neighbors** — *what lives nearby*
[[Pull-Based Deployment]] uses the same pull-on-schedule shape, and per-job log paths support [[Structured Logging]] habits.

**Clash** — *what pushes against this*
It is macOS-only and the plist format is easy to get subtly wrong, in which case the job just never loads, another flavour of [[Silent Failure]].
