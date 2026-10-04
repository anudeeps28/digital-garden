---
type: atomic
tags: [coding/database, coding/patterns, coding/distributed-systems]
date: 2026-10-04
---

# Store UTC, Display Local

## Idea
Store moments in time as UTC instants, keep each user's time zone as a named zone, and convert to local time only at the moment you show it.

## Definition
An **instant** is a single point on the global timeline: an epoch timestamp or a UTC datetime. Store and compare only instants; then sorting, durations and "has this passed?" are always correct regardless of where servers or users are. A user's location is stored separately as an **IANA zone ID** like `Europe/London` or `Asia/Kolkata`, never as a fixed offset like `+01:00`, because offsets change with daylight saving time and with law, and only the zone ID knows its history. Conversion to local time happens at the edge, in the UI or the report. A few practical traps: when computing a local "day" from UTC, offsets can push the boundary across midnight, so wrap the hour arithmetic instead of assuming the date stays the same. Abbreviations like `IST` or `CST` are ambiguous across countries, so override confusing ones with clearer labels. And for things that are genuinely local, like "remind me at 9am every day", store the local time plus the zone, and compute each instant when needed.

## Source
A long-standing engineering convention rather than one person's idea. It rests on the tz database, started by Arthur David Olson in 1986 and now maintained by IANA (Paul Eggert), and on UTC as standardised in 1960-1972. ISO 8601 (1988) provides the interchange format.

---

## Compass

**Roots** — *where this comes from*
It is [[Single Source of Truth]] applied to time: one canonical representation in storage, many views derived from it.

**Paths** — *where this leads*
Keeping conversion at the edge mirrors [[Persist Facts, Derive State]], and the conversion code is best kept in [[Pure Functions]] with tests for DST changes.

**Neighbors** — *what lives nearby*
[[JSON]] has no date type, so APIs should send ISO 8601 strings with a `Z` or offset. [[PostgreSQL]]'s `timestamptz` stores exactly this kind of instant.

**Clash** — *what pushes against this*
Future events in local time (a meeting at 10:00 next year) break the rule, since a government can change the offset before then. For those, the local time plus zone is the real fact.
