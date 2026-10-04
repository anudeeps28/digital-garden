---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Binary Search

## Idea
Binary search finds a target in sorted data by checking the middle and throwing away the half that cannot contain it, so a million items take about twenty steps.

## Definition
Keep two bounds, `lo` and `hi`, look at `mid`, and move one bound past `mid` depending on the comparison; each step halves the range, giving O(log n). The hard part is not the idea but the boundaries: whether `hi` is inclusive, whether the loop is `lo < hi` or `lo <= hi`, and whether you return `lo` or `mid`. Pick one convention and hold a clear **invariant** ("the answer is always in [lo, hi]"). The powerful generalisation is **binary search on the answer**: whenever a yes/no question is monotonic (false, false, ..., true, true), you can binary search for the boundary even without a sorted array. Integer square root asks "is mid² ≤ x?"; first and last position of a value searches for two boundaries; a rotated sorted array works because at least one half around `mid` is always sorted. The same trick finds the minimum capacity or speed that satisfies a constraint.

## Source
John Mauchly described binary search in the 1946 Moore School Lectures. Early published versions only worked for arrays of length 2ⁿ − 1 until Derrick Henry Lehmer published a general version in 1960. Joshua Bloch's 2006 post "Nearly All Binary Searches and Mergesorts are Broken" showed that `(lo + hi) / 2` overflows on large arrays, a bug that sat in the Java library for nine years.

---

## Compass

**Roots** — *where this comes from*
It needs sorted input, which is why it pairs with [[Sorting Algorithms]], and its O(log n) cost is the standard example of logarithmic growth in [[Big-O Notation]].

**Paths** — *where this leads*
A [[Binary Search Tree]] is binary search frozen into a data structure, so lookups stay logarithmic while inserts and deletes remain cheap, and database indexes extend the same idea to disk.

**Neighbors** — *what lives nearby*
The [[Two-Pointer Technique]] also walks sorted data from two ends but moves one step at a time, and `git bisect` in [[Git]] is binary search over commit history to find the one that introduced a bug.

**Clash** — *what pushes against this*
For lookups by exact key, a [[Hash Table]] gives O(1) and needs no sorting, so binary search wins only when you also need ordering, ranges, or the nearest value.
