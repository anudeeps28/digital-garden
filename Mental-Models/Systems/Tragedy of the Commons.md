---
type: atomic
tags: [mental-model, systems-thinking, system-trap, economics]
date: 2026-10-23
---

# Tragedy of the Commons

## Idea
When everyone can use a shared resource and the cost of overuse is spread across all users, each person's sensible extra use adds up to destroying it.

## Definition
A herder adding one more cow to a shared pasture gets the whole benefit of that cow but bears only a fraction of the damage to the grass. Every herder faces the same arithmetic, so the pasture is overgrazed. The structure needs three things: a shared resource, users who capture the gains individually, and feedback about the damage that is weak or late. Fisheries, clean air, open-source maintainers' time, a team's shared on-call rotation and a common codebase all fit. Meadows lists three fixes: educate and persuade people to restrain themselves, privatize the resource so each user bears their own costs, or regulate access with mutually agreed rules and enforcement.

## Source
Garrett Hardin, "The Tragedy of the Commons", *Science* (1968), building on William Forster Lloyd's 1833 pamphlet on overgrazing. Meadows, *Thinking in Systems*, Chapter 5, trap #2. Elinor Ostrom's *Governing the Commons* (1990, Nobel 2009) showed that communities often manage commons well through local rules, which Hardin's version underplayed. See [[Thinking in Systems]].

---

## Compass

**Roots** — *where this comes from*
It is [[Bounded Rationality]] meeting a [[Stock-Limited vs Flow-Limited Resources|flow-limited resource]]: each user sees their own gain clearly and the shared depletion only vaguely.

**Paths** — *where this leads*
The fixes work through [[Information Flows Shape Behavior]] (make the damage visible), through rules (a rung of [[Leverage Points]]), and through locating responsibility, an idea from [[Dancing with Systems]].

**Neighbors** — *what lives nearby*
[[Zero-Sum vs Positive-Sum Games]] is close: a commons starts positive-sum and becomes negative-sum once overused. [[Thundering Herd]] is a tragedy of the commons on a shared server, where every client's retry is reasonable and together they bring it down.

**Clash** — *what pushes against this*
Ostrom's research is the main counterweight. Real communities avoid the tragedy surprisingly often, with neither privatization nor top-down control, which means Hardin's "inevitable" applies only when trust and local rules are absent.
