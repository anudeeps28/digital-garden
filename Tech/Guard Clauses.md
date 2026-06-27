---
type: atomic
tags: [coding/patterns, error-handling, mental-model]
date: 2026-02-23
---

# Guard Clauses

## Idea
Check preconditions at the very start of a method and exit immediately if they fail — the bouncer at the door, not a check buried deep inside the room.

## Definition
A guard clause is an early return or throw at the top of a method that validates inputs before any real work begins. Instead of wrapping logic in nested `if` blocks, you invert the condition and exit immediately. This keeps the "happy path" code flat and readable, and ensures bad data never reaches the core logic.

```csharp
// Guard clause style
ArgumentException.ThrowIfNullOrWhiteSpace(documentText);
if (templates.Count == 0) return MatchResult.Empty;

// Now the real work — no nesting needed
```

## Source
C# coding session — `ArgumentException.ThrowIfNullOrWhiteSpace()`, input validation patterns

---

## Compass

**Neighbors** — *what lives nearby*
Guard clauses are the implementation of [[Fail Fast Fail Loudly]], and they embody the spirit of preconditions and design by contract — validating assumptions about your inputs before proceeding.

**Clash** — *what pushes against this*
Deep nested conditionals (`if valid { if not empty { if ... } }`) and optimistic execution that skips validation and trusts the caller both contradict the guard clause approach.

**Roots** — *where this comes from*
Guard clauses address fundamental questions about method design — how should a method handle bad input? This ties to [[One Method One Responsibility]], where a method that validates and processes is doing too much.

**Paths** — *where this leads*
Guard clauses create flat, readable "happy path" code where bad data never reaches the core logic, which embodies [[Fail Fast Fail Loudly]]. They also work naturally with the [[Try Pattern]], which handles cases where failure is expected and shouldn't throw.
