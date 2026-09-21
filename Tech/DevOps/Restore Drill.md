---
type: atomic
tags: [devops, coding/database, coding/testing]
date: 2026-09-16
---

# Restore Drill

## Idea
Nobody has a backup problem. Everybody has a restore problem — and you only find out which kind you have on the worst day of the year.

## Definition
A restore drill is a rehearsed, timed exercise in bringing a system back from its backups into a scratch environment, verifying the data is complete and the application actually runs against it. It exists because backup success is measured by the backup job's exit code, which tells you a file was written and nothing about whether that file can be read back into a working system. The drill produces two numbers worth more than the backup configuration itself: how long recovery actually took, and how much data was lost between the last usable copy and the incident. Those are the real recovery time and recovery point objectives, as opposed to the ones written in a document. It's also the only honest way to discover that the restore depends on a credential, a schema version, or an encryption key that no longer exists.

## Source
Long-standing operations practice; formalized in site reliability engineering — Google's SRE book makes the point that an untested restore procedure is not a recovery plan.

---

## Compass

**Roots** — *where this comes from*
The drill is the verification step that [[Geo-Redundant Backup]] and [[Customer-Managed Keys (CMK)]] both quietly depend on.

**Paths** — *where this leads*
Running one on a schedule converts disaster recovery from a document into a tested capability — the same move [[We Learn by Doing, Not by Watching]] describes for skills.

**Neighbors** — *what lives nearby*
[[Integration Tests]] prove the parts work together in normal conditions; a restore drill proves they can be reassembled from nothing.

**Clash** — *what pushes against this*
Drills cost real time and real money and produce no visible feature. They are the first thing cut, which is precisely why untested backups are the norm.
