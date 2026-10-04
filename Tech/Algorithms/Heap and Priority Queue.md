---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Heap and Priority Queue

## Idea
A priority queue always hands you the smallest (or largest) item next, and a binary heap implements it so that both adding and removing cost only O(log n).

## Definition
A **binary heap** is a complete binary tree stored in a plain array, where every parent is no larger than its children (a **min-heap**) or no smaller (a **max-heap**). The children of index `i` live at `2i + 1` and `2i + 2`, so no pointers are needed. Insert appends at the end and "sifts up"; removing the top swaps in the last element and "sifts down". Peeking at the top is O(1), and building a heap from an existing array is O(n). Typical uses: **kth largest element** keeps a min-heap of size k, so the root is the answer; **median of a stream** uses two heaps, a max-heap for the lower half and a min-heap for the upper half, kept balanced so the median sits at one or both roots; **meeting rooms II** sorts meetings by start time and keeps a min-heap of end times, where the heap's peak size is the number of rooms needed. Python's `heapq` is a min-heap, so you negate values for a max-heap.

## Source
J. W. J. Williams introduced the binary heap together with heapsort in "Algorithm 232: Heapsort" (Communications of the ACM, 1964). Robert W. Floyd published the same year an improvement that builds a heap in linear time.

---

## Compass

**Roots** — *where this comes from*
It is a tree with a weaker ordering rule than a [[Binary Search Tree]], just enough to find the minimum fast, and heapsort is one of the O(n log n) [[Sorting Algorithms]].

**Paths** — *where this leads*
Dijkstra's shortest path and [[A-Star Search]] both depend on a priority queue to always expand the most promising node next, which is how [[Breadth-First and Depth-First Search]] generalises to weighted graphs.

**Neighbors** — *what lives nearby*
A plain FIFO queue from [[Stack and Queue]] orders by arrival; a priority queue orders by importance. Job schedulers and a [[Message Broker]] with message priorities are the production versions.

**Clash** — *what pushes against this*
A heap cannot search for an arbitrary element or iterate in order without destroying itself, and if you only ever need the single minimum once, a linear scan is simpler than any structure in [[Big-O Notation]] terms.
