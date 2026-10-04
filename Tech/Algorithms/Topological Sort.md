---
type: atomic
tags: [coding/algorithms, devops, learning]
date: 2026-10-04
---

# Topological Sort

## Idea
A topological sort lines up tasks so that every task comes after everything it depends on, and it fails exactly when the dependencies contain a cycle.

## Definition
Model the tasks as a **directed graph** with an edge from A to B when A must happen before B. A topological order exists only if the graph is a **DAG** (directed acyclic graph). **Kahn's algorithm** counts each node's incoming edges, starts with the nodes that have none, and repeatedly removes a ready node, decrementing its neighbours' counts and adding any that drop to zero. If you finish having output fewer nodes than exist, there is a cycle. The **DFS approach** visits each node, recurses into its dependencies, and appends the node after they finish; reversing that finish order gives a valid ordering, and seeing a node that is "in progress" again means a cycle. Course Schedule is the canonical problem: courses are nodes, prerequisites are edges, and the question "can you finish them all?" is simply "is there a cycle?". Both methods run in O(V + E).

## Source
Arthur B. Kahn, "Topological sorting of large networks" (Communications of the ACM, 1962), written to order PERT project-scheduling networks. The DFS-based method was described by Robert Tarjan in 1976.

---

## Compass

**Roots** — *where this comes from*
It is a direct application of [[Breadth-First and Depth-First Search]]: Kahn's algorithm is BFS over ready nodes using a queue from [[Stack and Queue]], and the other version is DFS finishing order.

**Paths** — *where this leads*
Build tools, package managers and the stages of a [[CI-CD Pipeline]] are DAGs that get topologically sorted before running, and [[Database Migrations]] must run in dependency order for the same reason.

**Neighbors** — *what lives nearby*
[[Union-Find]] detects cycles in undirected graphs, while topological sort is the tool for directed ones. Spreadsheet recalculation and dependency-injection containers also resolve order this way.

**Clash** — *what pushes against this*
Most DAGs have many valid orders, so relying on one specific order that "happens to work" is fragile; if two tasks truly must run in sequence, the edge has to be explicit.
