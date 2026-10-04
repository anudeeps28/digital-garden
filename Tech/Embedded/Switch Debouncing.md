---
type: atomic
tags: [coding/embedded, frontend]
date: 2026-10-04
---

# Switch Debouncing

## Idea
A mechanical button does not make one clean contact; it chatters for a few milliseconds, and a fast microcontroller sees every bounce as a separate press. Debouncing filters those false edges in hardware or software.

## Definition
When metal contacts close they rebound several times before settling, producing a burst of transitions typically lasting from under a millisecond to tens of milliseconds. Read naively, one press counts as five. **Hardware debouncing** smooths the signal with an **RC filter** and squares it up again with a **Schmitt trigger**, whose two thresholds (hysteresis) stop a slowly changing voltage from toggling the output. **Software debouncing** accepts a new state only after it has been stable: sample the pin every few milliseconds and require N matching reads in a row, run a small counter that saturates, or wait a fixed delay after the first edge before reading again. Clean versions are tiny [[Finite State Machine|state machines]] (released, maybe-pressed, pressed, maybe-released) driven by a periodic timer rather than by blocking delays. If an [[Interrupt Service Routine]] is triggered on the pin, it should start the debounce timer, not count the press directly.

## Source
Jack Ganssle's "A Guide to Debouncing" (2004) measured real switches' bounce times and compared the hardware and software techniques; it remains the standard reference. Schmitt's trigger circuit dates from Otto Schmitt (1938).

---

## Compass

**Roots** — *where this comes from*
It begins with reading a [[GPIO and Open-Drain Outputs|GPIO]] input and discovering that the physical world is noisier than the logic levels suggest.

**Paths** — *where this leads*
Treating the button as a small state machine generalises into the [[Finite State Machine]] approach used for the whole controller.

**Neighbors** — *what lives nearby*
UI debounce and throttle are the same idea for keystrokes and scroll events, and [[Rate Limiting]] applies it to requests: collapse a burst into the one event you actually meant.

**Clash** — *what pushes against this*
Every debounce adds latency, and too long a window drops genuine fast presses, so the setting is a trade-off between responsiveness and false triggers rather than a fixed constant.
