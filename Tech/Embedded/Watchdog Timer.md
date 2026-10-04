---
type: atomic
tags: [coding/embedded, coding/architecture]
date: 2026-10-04
---

# Watchdog Timer

## Idea
A watchdog is a hardware countdown that resets the system unless the software keeps proving it is alive. More generally, it is the habit of checking that an expected event really arrived before a deadline, and moving to a safe state when it did not.

## Definition
A **watchdog timer** counts down independently of the CPU. Healthy firmware "kicks" (refreshes) it periodically; if the code hangs in a loop, deadlocks or crashes, the kicks stop, the counter hits zero, and the watchdog forces a reset. A **window watchdog** also complains if the kick comes too early, which catches code that is running but running wrong. The key design rule is to kick only from a place that proves real progress, such as the end of a full main-loop pass after every task has checked in, never from a timer interrupt that keeps firing while the rest of the system is stuck. The same pattern scales up as a software **deadline monitor**: "the sensor interrupt must arrive every 10 ms; if two are missed, flag a fault and enter the safe state". A worked example: a control loop expected a periodic data-ready interrupt from a sensor; adding a check that the interrupt count advanced each cycle turned a silent freeze into a logged fault and a clean shutdown.

## Source
Watchdogs have been used in spacecraft and industrial controllers for decades (Voyager's command computer, for example, switched to a backup when the attitude computer's heartbeat stopped for about ten seconds). I could not verify who first coined the term. Jack Ganssle's embedded writing is a widely cited practical guide to designing them well.

---

## Compass

**Roots** — *where this comes from*
It is hardware enforcement of [[Fail Fast Fail Loudly]]: a hang is the worst kind of failure because nothing reports it, and the watchdog turns it into a visible reset.

**Paths** — *where this leads*
Watchdogs and deadline monitors are core diagnostic mechanisms in [[Functional Safety]], and their resets should be logged so a [[Postmortem]] can count them.

**Neighbors** — *what lives nearby*
A cloud [[Health Probe]] is the same idea at service scale, and the distinction in [[Fault-vs-Failure]] explains the goal: catch the fault before it becomes a failure the user sees.

**Clash** — *what pushes against this*
A reset can hide the bug that caused it, turning a crash into a [[Silent Failure]] that recurs forever, and a reset loop can be worse than a stuck device if the safe state was never defined.
