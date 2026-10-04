---
type: atomic
tags: [coding/architecture, coding/patterns, coding/embedded]
date: 2026-10-04
---

# Finite State Machine

## Idea
Model the system as a small set of named states, the events it can receive, and the transitions each event causes. Behaviour that was hidden in a tangle of boolean flags becomes a table you can read and check.

## Definition
A **finite state machine (FSM)** is always in exactly one of a fixed set of **states**. When an **event** arrives, a **transition** rule decides the next state, possibly guarded by a condition and usually with an **action** attached. In a **Moore machine** outputs depend only on the current state; in a **Mealy machine** they depend on the transition. In code it is often a `switch` on the current state inside a loop or event handler, or a table of `(state, event) -> (next state, action)`. Its strength is that every combination is explicit: you can ask "what happens if *Stop* arrives while *Calibrating*?" and the answer is either in the table or visibly missing. FSMs are the standard shape for embedded control loops, protocol handlers (idle, sending, waiting for ack, retry), UI flows (empty, loading, loaded, error) and robots. A worked example: a whack-a-mole robot became reliable once it was rewritten from nested flags into four states (searching, aiming, striking, recovering), each with a timeout that led back to searching.

## Source
McCulloch and Pitts described finite automata in 1943; George Mealy (1955) and Edward Moore (1956) defined the two machine types used today. David Harel's statecharts (1987) added nesting and concurrency and became UML state machines.

---

## Compass

**Roots** — *where this comes from*
Events typically come from an [[Interrupt Service Routine]] or a message queue, and each state handler stays flat with [[Guard Clauses]] instead of deep nesting.

**Paths** — *where this leads*
A [[Reducer Pattern|reducer]] is an FSM written as a [[Pure Functions|pure function]] from (state, event) to new state, and [[Functional Safety]] work leans on FSMs because a safe state can be named and reached from everywhere.

**Neighbors** — *what lives nearby*
[[Switch Debouncing]] and [[Device Driver]] protocol sequences are small FSMs, and the Gang of Four State pattern in [[Design Patterns (Gang of Four)]] is the object-oriented way to write one.

**Clash** — *what pushes against this*
Flat FSMs suffer state explosion as features combine, which is why hierarchical statecharts exist, and for simple linear flows a state machine is ceremony that plain sequential code does not need.
