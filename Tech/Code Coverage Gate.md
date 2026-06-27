---
type: atomic
tags: [devops, coding/testing]
date: 2026-06-26
---

# Code Coverage Gate

## Idea
A pipeline tripwire: if too little of the code is tested, the build refuses to go green.

## Definition
A code coverage gate is a check in the [[CI-CD Pipeline]] that measures how much of the code is executed by tests and **fails the build** if line coverage drops below a threshold (around 75% on the KBA AI Document Ingestion project). Coverage is collected from the [[xUnit]] runs and the [[Jest]] runs, then compared to the bar before any [[Build Artifacts]] are published. It's a concrete instance of [[Fail Fast Fail Loudly]] — it stops undertested code from ever reaching a [[Release Stages|release stage]]. It measures quantity of coverage, not quality, so it complements rather than replaces [[Code Rabbit]] review and [[CodeQL]] scanning.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[CodeQL]] is another automated CI gate that can block the build, and both enforce the [[Fail Fast Fail Loudly]] principle to catch issues early.

**Clash** — *what pushes against this*
[[Pre-deploy Approvals]] represent a human gate operating in contrast to this automated metric gate, trading flexibility for strict numerical enforcement.

**Roots** — *where this comes from*
This gate is a stage within the broader [[CI-CD Pipeline]] — the multi-stage pipeline where this automated check lives.

**Paths** — *where this leads*
[[Build Artifacts]] are only produced once coverage clears the bar, making the gate a prerequisite to downstream release steps.
