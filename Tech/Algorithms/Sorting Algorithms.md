---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Sorting Algorithms

## Idea
Any sort that works only by comparing pairs of items needs at least about n log n comparisons, and the algorithms worth knowing differ mainly in how they reach that bound and what they trade for it.

## Definition
**Comparison sorts** decide order only by asking "is a < b?". A decision-tree argument shows they need Ω(n log n) comparisons in the worst case, because there are n! possible orders and each comparison at best halves them. **Merge sort** splits, sorts halves and merges, guaranteeing O(n log n) but using O(n) extra memory. **Quicksort** partitions around a pivot and is usually fastest in practice, with an O(n²) worst case that random pivots make unlikely. **Heapsort** is O(n log n) and in place. Simple sorts like insertion sort are O(n²) but excellent on tiny or nearly sorted input. **Non-comparison sorts** beat the bound by using the keys themselves: **counting sort** tallies small integers, **radix sort** sorts digit by digit, and **bucket (bin) sort** scatters values into ranges. Two properties matter when choosing: **stability** (equal keys keep their original order, needed when sorting by one field after another) and **in-place** operation (O(1) extra memory). Real libraries use hybrids such as Timsort (merge plus insertion) and introsort (quick plus heap plus insertion).

## Source
John von Neumann wrote merge sort in 1945; Tony Hoare invented quicksort in 1959 (published 1961); radix sorting dates to Herman Hollerith's punched-card tabulators of the 1880s. Donald Knuth's *The Art of Computer Programming, Vol. 3: Sorting and Searching* (1973) is the classic reference, and Tim Peters wrote Timsort for Python in 2002.

---

## Compass

**Roots** — *where this comes from*
The n log n lower bound is the most famous proof in [[Big-O Notation]], and merge sort and quicksort are [[Recursion]] used as divide and conquer.

**Paths** — *where this leads*
Sorting first is often what unlocks [[Binary Search]] and the [[Two-Pointer Technique]], and sorting by start time is the first step of interval problems such as meeting rooms.

**Neighbors** — *what lives nearby*
Heapsort is the [[Heap and Priority Queue]] used to drain items in order, and an in-order walk of a [[Binary Search Tree]] produces sorted output for free.

**Clash** — *what pushes against this*
If you only need the top k items or a membership check, a full sort is wasted work; a heap or a [[Hash Table]] does it with less.
