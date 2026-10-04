---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Breadth-First and Depth-First Search

## Idea
BFS explores a graph level by level from the start, while DFS follows one path as deep as it can before backing up; together they are the two basic ways to visit everything reachable.

## Definition
**BFS** uses a queue: visit the start, enqueue its neighbours, and process them in arrival order. Because it reaches nodes in order of distance, BFS finds the **shortest path in an unweighted graph**, such as the fewest moves through a grid or the fewest hops between two people. **DFS** uses a stack, usually the call stack via recursion: go to a neighbour, then its neighbour, and only back up when stuck. DFS is natural for exhaustive exploration, cycle detection and anything that needs a finishing order. Both need a **visited** set so cycles do not loop forever, and both run in O(V + E). Number of islands is the classic grid problem: scan every cell, and each time you find unvisited land, flood-fill it with BFS or DFS and count one island. Pacific Atlantic water flow inverts the search: start from each ocean's edge and walk "uphill", then return cells reached from both sides.

## Source
Konrad Zuse described BFS in his 1945 (rejected, published 1972) thesis on Plankalkül; Edward F. Moore reinvented it in 1959 for shortest paths through a maze, and C. Y. Lee applied it to wire routing in 1961. DFS traces back to Charles Pierre Trémaux's 19th-century maze-solving method, and Robert Tarjan and John Hopcroft established it as a core graph algorithm in the early 1970s.

---

## Compass

**Roots** — *where this comes from*
BFS is a queue and DFS is a stack, so both are direct applications of [[Stack and Queue]], and recursive DFS is [[Recursion]] on a graph.

**Paths** — *where this leads*
DFS finishing order gives a [[Topological Sort]], and replacing the BFS queue with a [[Heap and Priority Queue|priority queue]] yields Dijkstra's algorithm and, with a heuristic, [[A-Star Search]].

**Neighbors** — *what lives nearby*
[[Union-Find]] answers the same connected-components question incrementally as edges arrive, and tree traversals on a [[Binary Search Tree]] are DFS (pre, in, post-order) and BFS (level order) on a special graph.

**Clash** — *what pushes against this*
Plain BFS is wrong once edges have different weights, and recursive DFS can overflow the stack on large grids, so iterative versions are safer in production.
