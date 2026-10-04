---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Big-O Notation

## Idea
Big-O describes how the cost of an algorithm grows as its input grows, so you can tell whether a solution will survive ten times more data before you write it.

## Definition
**Big-O** gives an upper bound on growth, ignoring constants and smaller terms: a loop over `n` items is O(n), a loop inside a loop is O(n²), halving the search space each step is O(log n). It answers "what happens when `n` gets large?", not "how fast is this today?". The common ladder is O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ), and the jump between rungs matters far more than micro-tuning within one. A useful habit is to estimate the complexity before optimising anything. If `n` is 10⁵ and your idea is O(n²), that is 10¹⁰ operations and no clever caching will save it; an O(n log n) idea finishes instantly. **Space complexity** works the same way for memory. Related notation fills in the picture: **Big-Ω** is a lower bound and **Big-Θ** a tight bound, though everyday usage says "Big-O" for all three.

## Source
The O symbol comes from number theory: Paul Bachmann introduced it in 1894 and Edmund Landau popularised it in 1909 (hence "Landau symbols"). Donald Knuth brought it into computer science and defined Ω and Θ for algorithm analysis in "Big Omicron and Big Omega and Big Theta" (SIGACT News, 1976).

---

## Compass

**Roots** — *where this comes from*
It is the shared vocabulary of [[Programming Interview Preparation]], where every answer is expected to state its time and space cost, and it underlies how [[Scalability-and-Load-Parameters|load parameters]] are reasoned about in real systems.

**Paths** — *where this leads*
Knowing the target complexity points you to the right tool: O(log n) suggests [[Binary Search]] or a [[Heap and Priority Queue|heap]], O(1) lookups suggest a [[Hash Table]], and an exponential brute force is often a sign that [[Dynamic Programming]] can collapse it.

**Neighbors** — *what lives nearby*
[[Sorting Algorithms]] are the classic case study, since the O(n log n) lower bound for comparison sorts is a Big-O argument, and [[Recursion]] costs are usually found by counting calls in the recursion tree.

**Clash** — *what pushes against this*
Big-O hides constants and real hardware effects, so an O(n) algorithm with poor cache behaviour can lose to an O(n log n) one at realistic sizes. In production, users feel [[Percentile-Based-Performance-Metrics|tail latency]], which no asymptotic bound captures.
