---
type: atomic
tags: [mental-model, coding/patterns, coding/quality]
date: 2026-10-04
---

# Rule of Three

## Idea
Tolerate duplication twice; extract a shared abstraction on the third copy, once you can see what the copies really have in common.

## Definition
The first time you write something, just write it. The second time, you notice the duplication and write it again anyway. The third time, you refactor. The reasoning is that two examples are not enough to tell which parts are essential and which are coincidence, so an abstraction drawn from two copies is usually the wrong shape and has to be bent later. Three copies give you a pattern. The rule is a heuristic, not a law, and the third copy is where the real judgement starts: extraction removes drift between copies but creates a shared dependency, so a change to the helper now touches every caller. A worked example: three API routers each carried byte-for-byte identical helper functions. Extracting them was clearly right on duplication grounds, but it also meant one edit could now break all three routers at once, so the extraction went in with tests around each caller rather than as a quick cut-and-paste.

## Source
Attributed to Don Roberts and popularised by Martin Fowler in *Refactoring: Improving the Design of Existing Code* (1999), as "Three strikes and you refactor."

---

## Compass

**Roots** — *where this comes from*
It is a guard rail on [[One Method One Responsibility]]: extract when a responsibility has clearly emerged, not before. It also lives inside [[First Make It Work, Then Make It Better]], since the first two copies are the "make it work" phase.

**Paths** — *where this leads*
The third copy is the moment to consider a [[Shared Module Library]] or a [[Shared Contract Package]], and to weigh the growing [[Blast Radius]] of the shared code against the drift it prevents.

**Neighbors** — *what lives nearby*
[[Turn Repeated Work Into a Skill]] applies the same count to workflows rather than code, and [[Design Patterns (Gang of Four)]] are what many third-copy extractions turn out to be.

**Clash** — *what pushes against this*
Some duplication is dangerous from the first copy, such as security checks or business rules that must never disagree, and waiting for three is how they drift. The opposite risk is also real: extracting at three can still be premature if the copies are only alike by accident.
