---
type: atomic
tags: [coding/algorithms, coding/python, learning]
date: 2026-10-04
---

# Dynamic Programming

## Idea
Dynamic programming solves a problem by breaking it into overlapping subproblems, solving each one once, and reusing the stored answers instead of recomputing them.

## Definition
A problem suits DP when it has **optimal substructure** (the best answer is built from best answers to smaller pieces) and **overlapping subproblems** (the same pieces come up again and again). There are two ways in. **Memoization** is top-down: write the natural recursion and cache each result the first time you compute it. **Tabulation** is bottom-up: fill a table from the smallest cases upward so every value you need already exists. Climbing Stairs is the starter example: the ways to reach step `n` equal ways(n−1) + ways(n−2), which is exponential when written as plain recursion and linear once cached. Maximum Subarray (Kadane's algorithm) shows DP shrunk to two variables: at each element, either extend the previous run or start fresh. One Python trap is worth remembering: `def f(n, memo={})` creates the default dict once, at definition time, so the cache silently persists across separate calls. Pass the cache explicitly or use `functools.lru_cache`.

## Source
Richard Bellman developed and named dynamic programming at RAND in the early 1950s; the term first appears in "On the Theory of Dynamic Programming" (PNAS, 1952), followed by his book *Dynamic Programming* (1957). Bellman later wrote that he picked the name partly to sound unmathematical to a research-averse Secretary of Defense. Donald Michie coined "memoization" in 1968. Kadane's algorithm is credited to Jay Kadane (1977) and was popularised by Jon Bentley's *Programming Pearls* (1984).

---

## Compass

**Roots** — *where this comes from*
DP is [[Recursion]] that remembers: the memo table is the difference between an exponential recursion tree and a linear walk.

**Paths** — *where this leads*
The same idea of trading memory for recomputation scales up to [[In-Memory Caching]] in services, where expensive results are stored and served again rather than rebuilt per request.

**Neighbors** — *what lives nearby*
The memo is usually a [[Hash Table]] keyed by the subproblem's arguments, and estimating states times work-per-state in [[Big-O Notation]] tells you whether a DP formulation is fast enough. Many array DPs, like Kadane's, sit close to the [[Sliding Window]] pattern.

**Clash** — *what pushes against this*
A [[Pure Functions|pure function]] is a requirement, not a nicety: if the result depends on hidden state, cached answers become wrong answers. Greedy algorithms clash too, because when a greedy choice is provably safe, DP is unnecessary overhead.
