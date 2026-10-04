---
type: atomic
tags: [coding/architecture, coding/patterns, coding/python]
date: 2026-10-04
---

# Pure Functions

## Idea
A pure function's output depends only on its inputs, and calling it changes nothing else in the world. Same arguments in, same answer out, every time.

## Definition
A function is **pure** when it has two properties. It is **deterministic**: no hidden inputs like the current time, a global variable, a random number or a file. And it has **no side effects**: it doesn't mutate its arguments, write to disk, log, or send anything. Together these give **referential transparency**: you can replace a call with its result without changing the program. In practice the hardest part is not mutating inputs. Instead of appending to the list you were given, return a new list; instead of setting a field, return a copy with the field changed. Languages help here. In Python, a `@dataclass(frozen=True)` raises an error on assignment, and `dataclasses.replace(obj, field=value)` returns the updated copy. It's worth testing immutability explicitly: call the function, then assert the original input is unchanged, because an accidental in-place edit is exactly the bug that slips through tests checking only the return value. Anything that needs the clock or randomness can still be pure if you pass "now" or the random seed in as a parameter.

```python
@dataclass(frozen=True)
class Session:
    remaining: int

def tick(s: Session, seconds: int) -> Session:
    return replace(s, remaining=max(0, s.remaining - seconds))
```

## Source
The concept comes from the mathematical definition of a function and from functional programming; "referential transparency" was brought into programming by Christopher Strachey in his 1967 lecture notes "Fundamental Concepts in Programming Languages", borrowing the term from philosopher W. V. O. Quine. Haskell (1990) made purity a language default.

---

## Compass

**Roots** — *where this comes from*
It is the code-level form of [[Read-Only by Default]]: never change what you were handed. In [[Python]], frozen dataclasses make that a rule the runtime enforces rather than a habit.

**Paths** — *where this leads*
Pure functions are the building blocks of a [[Functional Core, Imperative Shell]] and of the [[Reducer Pattern]], and they are what make [[Unit Tests]] fast and mock-free.

**Neighbors** — *what lives nearby*
Immutable [[DTOs (Data Transfer Objects)]] are the natural data for pure functions to pass around. [[One Method One Responsibility]] keeps them small enough to reason about.

**Clash** — *what pushes against this*
A program that is entirely pure does nothing useful; at some point it must touch the world. Copying instead of mutating also costs memory and time for very large data, which is why performance-critical inner loops often stay mutable.
