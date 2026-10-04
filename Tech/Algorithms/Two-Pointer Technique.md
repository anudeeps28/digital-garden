---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Two-Pointer Technique

## Idea
Use two indices that move through the data in a coordinated way, so a problem that looks like it needs a nested loop can be solved in a single pass.

## Definition
There are three common shapes. **Opposite ends**: start one pointer at each end of a sorted array and move them inward based on a comparison; finding a pair that sums to a target works because if the sum is too small, only moving the left pointer can help. 3Sum builds on this by fixing one element and running a two-pointer scan on the rest, turning O(n³) into O(n²). **Read and write**: one pointer scans, the other marks where the next kept element goes, which removes duplicates from a sorted array in place with O(1) extra memory. **Gap or speed**: on a linked list, advance one pointer `n` steps ahead and then move both together to find the nth node from the end in one pass, or move one twice as fast to find the middle, which is the first step in checking whether a list is a palindrome. The common thread is that each pointer only ever moves forward, so the total work is linear.

## Source
A folklore technique with no single inventor; it appears throughout classic texts such as Knuth's *The Art of Computer Programming* and is now a named pattern in interview preparation. The fast-and-slow variant for cycle detection is attributed to Robert W. Floyd by Knuth (1969), though Floyd never published it as such.

---

## Compass

**Roots** — *where this comes from*
It exploits sorted order the same way [[Binary Search]] does, and it is a staple of [[Programming Interview Preparation]] because it shows you can beat the brute-force bound in [[Big-O Notation]].

**Paths** — *where this leads*
When both pointers move in the same direction and you care about what lies between them, the pattern becomes a [[Sliding Window]].

**Neighbors** — *what lives nearby*
Fast and slow pointers are the core trick for a [[Linked List]], where you cannot index into the middle, and in-place compaction is the same read/write idea used in partitioning steps of [[Sorting Algorithms]].

**Clash** — *what pushes against this*
On unsorted data, the opposite-ends version breaks, and a [[Hash Table]] solves pair-sum in one pass without sorting at the cost of extra memory.
