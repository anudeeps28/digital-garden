---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Union-Find

## Idea
Union-Find keeps track of which items belong to the same group and can merge two groups or ask "are these two connected?" in almost constant time.

## Definition
Also called a **disjoint-set union (DSU)**, it stores a forest where each node points to a parent and the root names the group. `find(x)` follows parents up to the root; `union(a, b)` attaches one root under the other. Two small optimisations make it extremely fast. **Path compression** points every node visited during `find` straight at the root, flattening the tree for next time. **Union by rank** (or by size) always hangs the shorter tree under the taller one so trees stay shallow. Together they give amortised O(α(n)) per operation, where α is the inverse Ackermann function, which is at most 4 for any input that fits in the universe. Number of connected components counts how many successful unions happen and subtracts from `n`. Graph valid tree checks that there are exactly `n − 1` edges and that no edge ever joins two nodes already in the same set, since that would form a cycle.

## Source
Bernard A. Galler and Michael J. Fischer, "An Improved Equivalence Algorithm" (Communications of the ACM, 1964). Robert Tarjan proved the O(α(n)) amortised bound with path compression and union by rank in 1975, and showed in 1979 that it is optimal for pointer-based structures.

---

## Compass

**Roots** — *where this comes from*
It answers the connected-components question that [[Breadth-First and Depth-First Search]] answers with a full traversal, but incrementally as edges arrive, and its near-constant cost is a striking result in [[Big-O Notation]].

**Paths** — *where this leads*
Kruskal's minimum spanning tree algorithm uses it to skip edges that would form a cycle, and it shows up in image segmentation, network connectivity and grouping duplicate records.

**Neighbors** — *what lives nearby*
It is a tree structure stored in an array, like the [[Heap and Priority Queue|binary heap]], and a [[Hash Table]] often maps real-world labels to its integer ids.

**Clash** — *what pushes against this*
It only merges; it cannot split a group or delete an edge, and for directed dependencies you need [[Topological Sort]] instead.
