---
type: atomic
tags: [mental-model, coding/patterns, architecture]
date: 2026-02-23
---

# Read-Only by Default

## Idea
Default to the most restrictive access and mutability level available — only open things up when there is a concrete reason to.

## Definition
Start with `private`, `readonly`, `IReadOnlyList`, `const` — the most locked-down option. Only relax the constraint when a specific need demands it. This prevents a whole class of bugs where data is accidentally modified somewhere unexpected, and makes intent explicit: if something is readable, that's a deliberate statement that it cannot change.

## Source
C# coding session — `private static readonly`, `IReadOnlyList<string>` vs `List<string>`, immutable records

---

## Compass

**Neighbors** — *what lives nearby*
This principle echoes [[Principle of Least Privilege]], which applies the same idea to permissions and access control in security contexts. It's closely related to [[Immutability as Design Choice]], which treats immutability as a deliberate structural decision. Both share the philosophy of [[Define Contract Before Implementation]], where constraints and safeguards are established upfront to make your intent explicit rather than implicit.

**Clash** — *what pushes against this*
The opposite approach is being permissive by default — making everything public and mutable everywhere. This often leads to "I'll restrict it later," a form of technical debt that rarely gets paid off and leaves systems vulnerable to accidental mutations.

**Roots** — *where this comes from*
This grows out of defensive programming, the broader practice of designing systems that are hard to break accidentally. It answers a foundational question: how do you structure code and data so that unexpected mutations become impossible rather than just unlikely?

**Paths** — *where this leads*
Embracing read-only-by-default yields easier reasoning — you know data is exactly what it was when created, with no surprise mutations elsewhere. It enables safer APIs where callers cannot mutate what they shouldn't. In C#, this translates to practical choices: prefer `IReadOnlyList<T>` over `List<T>` in method signatures, use `record` over `class` for data containers, and apply `private static readonly` consistently.
