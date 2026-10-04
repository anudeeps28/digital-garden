---
type: atomic
tags: [coding/algorithms, ai/robotics, ai]
date: 2026-10-04
---

# A-Star Search

## Idea
A* finds the cheapest path through a graph by always expanding the node that looks best overall: the cost already paid to reach it plus an optimistic guess of the cost still to go.

## Definition
For every node A* tracks **g(n)**, the cost of the best known path from the start, and estimates **h(n)**, a **heuristic** for the remaining cost to the goal. It scores nodes by **f(n) = g(n) + h(n)** and keeps the frontier in a priority queue ordered by f, always popping the lowest. When it pops the goal, it is done. If h never overestimates the true remaining cost (it is **admissible**), the path found is guaranteed optimal; if h is also **consistent** (obeys the triangle inequality), no node needs reopening. The heuristic is what makes A* fast: a good one steers the search straight toward the goal. Set h = 0 and A* becomes **Dijkstra's algorithm**, exploring outward in all directions. In robot navigation the map is an **occupancy grid** of free and blocked cells, g is distance travelled, and h is the straight-line (Euclidean) or Manhattan distance to the target. Inflating obstacles by the robot's radius before planning keeps the path physically drivable.

## Source
Peter Hart, Nils Nilsson and Bertram Raphael, "A Formal Basis for the Heuristic Determination of Minimum Cost Paths", IEEE Transactions on Systems Science and Cybernetics, 1968, developed at SRI for the Shakey robot. Dijkstra's shortest-path algorithm is from 1959.

---

## Compass

**Roots** — *where this comes from*
It is [[Breadth-First and Depth-First Search]] with a sense of direction, and it runs on a [[Heap and Priority Queue|priority queue]] keyed by f.

**Paths** — *where this leads*
A planned path is only useful once a [[Particle Filter]] knows where the robot is and a [[PID Controller]] keeps it on the line.

**Neighbors** — *what lives nearby*
Like [[Dynamic Programming]], it reuses the best cost found so far to each subproblem instead of recomputing it, and its complexity is analysed in [[Big-O Notation]] terms of branching and depth.

**Clash** — *what pushes against this*
On large or high-dimensional spaces (a robot arm's joint angles) the grid becomes impossibly large, and sampling-based planners such as RRT take over; an inadmissible heuristic is faster but gives up the optimality guarantee.
