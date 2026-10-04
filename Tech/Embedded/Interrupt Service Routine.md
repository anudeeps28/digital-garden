---
type: atomic
tags: [coding/embedded]
date: 2026-10-04
---

# Interrupt Service Routine

## Idea
An interrupt lets a hardware event stop the main program, run a small handler, and return as if nothing happened. The rule is to keep that handler short: note what happened, and let the main loop do the work.

## Definition
An **interrupt service routine (ISR)** is a function the CPU jumps to when a peripheral raises an interrupt: a timer overflowed, a byte arrived on a UART, a pin changed level on an **external interrupt line**. The CPU saves its context, looks up the handler in the **vector table**, runs it, and resumes the interrupted code. Priorities decide which interrupts may pre-empt others. Good ISRs are tiny: clear the interrupt flag, copy the data, set a flag or push into a ring buffer, and return. Anything slow (printing, long calculations, waiting) belongs in the main loop, because while an ISR runs, other events of equal or lower priority wait and can be lost. Variables shared between an ISR and the main loop must be **`volatile`**, and multi-byte updates need a brief critical section, or the main loop can read half an old value and half a new one.

```c
volatile bool button_pressed = false;
void EXTI0_IRQHandler(void) { EXTI->PR = 1; button_pressed = true; }
```

## Source
Interrupts appeared in the early 1950s: the UNIVAC 1103A (1953) is usually credited with the first, and the NBS DYSEAC (1954) used them for I/O (Mark Smotherman, "A History and Overview of Interrupts"). The "short ISR, defer the work" guidance is standard embedded practice, echoed in operating systems as top-half/bottom-half handling.

---

## Compass

**Roots** — *where this comes from*
The flags an ISR clears and the registers it reads are all [[Memory-Mapped IO]], and the alternative it replaces is polling a [[GPIO and Open-Drain Outputs|GPIO]] pin in a loop.

**Paths** — *where this leads*
Handing events from ISR to main loop naturally produces an event queue feeding a [[Finite State Machine]], and a missing interrupt is exactly what a [[Watchdog Timer]] is there to catch.

**Neighbors** — *what lives nearby*
Doing the minimum now and deferring the rest is the same instinct as the [[Outbox Pattern]], and a ring buffer between ISR and main loop is a fixed-size cousin of [[Stack and Queue|a queue]].

**Clash** — *what pushes against this*
Interrupts make timing non-deterministic and races hard to reproduce, so some safety-critical designs prefer strict time-triggered polling, as encouraged in [[Functional Safety]] work.
