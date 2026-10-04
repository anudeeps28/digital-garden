---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Stack and Queue

## Idea
A stack hands back the most recently added item first (last in, first out), and a queue hands back the oldest first (first in, first out); choosing between them decides the order in which work gets done.

## Definition
A **stack** supports push and pop at one end in O(1). It is the right tool whenever the latest thing opened must be the first closed. **Valid parentheses** pushes each opener and pops on each closer, failing on a mismatch. **Reverse Polish Notation** evaluation pushes numbers and, on an operator, pops two operands and pushes the result. A **min stack** stores the running minimum alongside each value so `getMin` is O(1). A **monotonic stack** keeps elements in increasing or decreasing order by popping anything that breaks the order, which answers "next greater element" and "daily temperatures" in one pass. A **queue** supports enqueue at the back and dequeue at the front in O(1), and it is what makes breadth-first search visit nodes in distance order. A **deque** allows both ends and powers sliding window maximum.

## Source
Alan Turing used a stack ("bury" and "unbury") for subroutine return addresses in his 1946 ACE design. Klaus Samelson and Friedrich L. Bauer proposed the "Kellerprinzip" (cellar principle) in 1955 and patented it in 1957 for compiling expressions in what became ALGOL; Charles Hamblin developed the same idea independently in Australia around 1957, alongside his work on Reverse Polish Notation.

---

## Compass

**Roots** — *where this comes from*
The program's call stack is a stack, which is why [[Recursion]] can always be rewritten with an explicit stack and why it is bounded by [[Stack vs Heap Memory|stack memory]].

**Paths** — *where this leads*
Queues are the backbone of [[Breadth-First and Depth-First Search]] and [[Topological Sort]], and at system scale a [[Message Broker]] is a durable queue between services.

**Neighbors** — *what lives nearby*
A [[Heap and Priority Queue|priority queue]] replaces arrival order with importance, and either structure can be implemented on a [[Linked List]] or a circular array.

**Clash** — *what pushes against this*
Strict FIFO is unfair once items have different urgency or cost, and an unbounded queue hides overload until memory runs out, which is the problem [[Backpressure]] exists to solve.
