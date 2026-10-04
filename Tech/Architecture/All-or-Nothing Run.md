---
type: atomic
tags: [coding/architecture, coding/patterns, workflow]
date: 2026-10-04
---

# All-or-Nothing Run

## Idea
Some jobs should abort completely on any error rather than deliver a partial result. Whether that is the right call depends mostly on whether a human is watching and can simply run it again.

## Definition
An **all-or-nothing run** treats the whole job as one unit: if any step fails, nothing is published and the run ends with a clear error. Consider a job that gathers items from several sources, asks an LLM to summarise them, and produces a daily digest that someone reads and acts on. If one source times out, or the model returns output that fails validation, the tempting move is to skip it and ship the rest. But a digest missing a section looks complete; the reader has no way to know what they didn't see, so a **partial result actively misleads**. Since a person triggers the run and re-running costs only a minute, aborting is cheap and honest. Contrast an unattended pipeline that syncs records overnight. Nobody is there to press "run again", so it should do the opposite: process what it can, retry the rest later, record exactly what is pending, and never lose data. The rule of thumb: **human in the loop and output read as a whole, prefer all-or-nothing; unattended and items independent, prefer best-effort with durable retries.**

## Source
The phrase "all or nothing" is how Jim Gray defined **atomicity** in "The Transaction Concept: Virtues and Limitations" (VLDB, 1981); Härder and Reuter folded it into the ACID acronym in 1983. Applying it to a whole batch job rather than a database transaction is a descriptive extension, not a separately coined pattern.

---

## Compass

**Roots** — *where this comes from*
It is the atomicity of [[ACID Properties]] lifted from a database transaction to an entire job, and it shares the instinct of [[Fail Fast Fail Loudly]]: an obvious failure beats a quiet wrong answer.

**Paths** — *where this leads*
Invalid model output becomes a hard stop once you add [[Structured Output Validation]], and a clear abort message is what lets the person at the keyboard decide what to do next.

**Neighbors** — *what lives nearby*
The unattended alternative leans on [[Idempotency]] and a [[Write Ledger]] so retries are safe. Partial results that look complete are a cousin of [[A Stale Source Is Confidently Wrong]].

**Clash** — *what pushes against this*
[[Graceful Degradation]] argues the opposite, that a working subset beats nothing, and for user-facing services it usually wins. All-or-nothing also widens the [[Blast Radius]] on purpose, so one flaky source can block every run until it is fixed.
