---
type: atomic
tags: [mental-model, systems-thinking, feedback]
date: 2026-10-23
---

# Delays Cause Oscillation

## Idea
When feedback arrives late, people keep correcting after the problem is already fixed, so the system overshoots and swings back and forth around its target.

## Definition
Every feedback loop has delays: time to notice, time to decide, time for the action to take effect. If you act on old information, you keep correcting after the correction has already worked. Think of turning a slow shower tap too hot, then too cold, or a central bank raising interest rates until a recession shows up a year later. Meadows' car-dealer example shows that reacting faster can make the swings worse. The fix is often to react more slowly and steadily, or to shorten the delay itself. Delays are not just friction. They decide whether a system is stable or keeps swinging.

## Source
Donella H. Meadows, *Thinking in Systems*, Chapter 2 ("A Brief Visit to the Systems Zoo", the car-dealership inventory model). The classic demonstration is MIT's Beer Game (Jay Forrester, 1960s), where players in a simple supply chain reliably produce wild inventory swings. See [[Thinking in Systems]].

---

## Compass

**Roots** — *where this comes from*
It is a [[Balancing Feedback Loop]] plus a time lag. The goal-seeking is still there, but the system sees its own state too late.

**Paths** — *where this leads*
Delays and buffers are a rung on [[Leverage Points]]. In practice the answer is usually to shorten information delays rather than react harder, which is why [[Information Flows Shape Behavior]].

**Neighbors** — *what lives nearby*
The [[PID Controller]] has a derivative term that reacts to how fast the error is changing, which damps exactly this overshoot. [[Delay Is Capacity Catching Up]] is a personal reading of the same thing: some delays are capacity still being built, not something to overreact to.

**Clash** — *what pushes against this*
Patience can be overdone. Some delays hide real problems, and waiting for perfect information means acting too late. That is especially true when a [[Reinforcing Feedback Loop]] is running and every period of delay compounds.
