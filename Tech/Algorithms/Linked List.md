---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Linked List

## Idea
A linked list stores items as separate nodes that each point to the next, so inserting or removing is cheap once you are at the right spot, but reaching that spot means walking from the head.

## Definition
Each node holds a value and a `next` pointer (plus `prev` in a **doubly linked list**). Insert and delete at a known node are O(1) because you just rewire pointers; access by index is O(n) because there is no random access. Most list problems are about pointer manipulation without losing track of nodes. **Reverse** a list by walking it with three pointers (`prev`, `curr`, `next`) and flipping each link. **Fast and slow pointers** solve several problems at once: when the fast one reaches the end, the slow one is at the **middle**; if they ever meet, the list has a **cycle** (Floyd's algorithm). **Reorder list** (first, last, second, second-to-last...) combines all three: find the middle, reverse the second half, then interleave. **Merge two sorted lists** walks both and links the smaller head each time, and a **dummy head node** avoids special-casing an empty result.

## Source
Allen Newell, Cliff Shaw and Herbert Simon invented the linked list in 1955 to 1956 at RAND as the core structure of their Information Processing Language (IPL), used for the Logic Theorist AI program. Floyd's cycle detection is attributed to Robert W. Floyd by Donald Knuth (1969).

---

## Compass

**Roots** — *where this comes from*
Nodes live wherever the allocator puts them, which ties the list to [[Stack vs Heap Memory|heap allocation]] and explains its poor cache behaviour compared with arrays.

**Paths** — *where this leads*
A [[Stack and Queue]] can be built on a linked list with O(1) push and pop, and the chains in a chained [[Hash Table]] are linked lists.

**Neighbors** — *what lives nearby*
The fast/slow trick is the [[Two-Pointer Technique]] adapted for structures you cannot index, and reversal is a common [[Recursion]] exercise.

**Clash** — *what pushes against this*
In practice, contiguous arrays usually win even for insert-heavy work because CPUs love sequential memory, which is a gap that [[Big-O Notation]] alone does not show.
