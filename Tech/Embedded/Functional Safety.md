---
type: atomic
tags: [coding/embedded, coding/architecture]
date: 2026-10-04
---

# Functional Safety

## Idea
Functional safety asks a narrow question: when a component in a system fails, does the system still avoid hurting anyone? It does not promise no failures; it promises that failures are detected and lead to a safe state.

## Definition
**Functional safety** is the part of overall safety that depends on electrical, electronic and software systems working correctly in response to their inputs. The process starts with **hazard analysis and risk assessment**: what can go wrong, how severe would it be, how often would people be exposed, and could they control it. The resulting risk sets an integrity level, a **SIL** (1 to 4) in the generic standard or an **ASIL** (A to D, with QM below for non-safety items) in automotive, and higher levels demand more rigour: stricter development processes, independent reviews, redundancy and higher **diagnostic coverage**, meaning the fraction of dangerous faults the system can detect at run time. Every safety function defines a **safe state** (motor off, valve closed, controlled stop) and a **fault tolerant time interval** within which a fault must be detected and that state reached. Typical mechanisms include [[Watchdog Timer|watchdogs]], RAM and flash self-tests, redundant sensors cross-checked against each other, and plausibility checks on inputs.

## Source
IEC 61508, "Functional safety of electrical/electronic/programmable electronic safety-related systems", first edition 1998 (second edition 2010), is the umbrella standard. ISO 26262 adapts it for road vehicles (first edition November 2011, second 2018) and introduced ASILs. Sector variants include IEC 62304 (medical software) and EN 50128 (rail).

---

## Compass

**Roots** — *where this comes from*
It formalises [[Fault-vs-Failure]]: faults are assumed to happen, and the engineering effort goes into stopping them from becoming hazardous failures.

**Paths** — *where this leads*
It pushes designs toward explicit [[Finite State Machine|state machines]] with a defined safe state, and toward [[Defence in Depth]] with independent layers of detection.

**Neighbors** — *what lives nearby*
[[Fail Fast Fail Loudly]] is the software habit behind it, and [[Blast Radius]] is the same thinking applied to deployments rather than physical harm.

**Clash** — *what pushes against this*
The process is heavy and expensive, and certification evidence can drift into paperwork for its own sake; it also says little about security, which modern connected devices need just as much.
