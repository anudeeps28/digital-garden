---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Recursion

## Idea
A recursive function solves a problem by calling itself on a smaller version of the same problem until it reaches a case simple enough to answer directly.

## Definition
Every recursive function needs two parts: a **base case** that returns without recursing, and a **recursive case** that shrinks the input and calls itself. Each call gets its own **stack frame** holding its arguments and local variables, so the call stack grows with recursion depth, and a missing or unreachable base case ends in a stack overflow. Recursion comes in several shapes. **Tail recursion** makes the recursive call the very last action, which some compilers turn into a loop. **Tree recursion** makes more than one call per step, as in naive Fibonacci or the Tower of Hanoi, where moving `n` discs means moving `n-1` discs twice, giving 2ⁿ − 1 moves. **Indirect recursion** has A call B which calls A, and **nested recursion** passes a recursive call as an argument to itself. Recursion is the natural fit for anything self-similar: trees, nested structures, divide-and-conquer sorts, and series such as computing a Taylor expansion term by term.

## Source
Recursive definitions are old mathematics (Dedekind and Peano in the 1880s; recursive function theory by Gödel, Kleene and Church in the 1930s). In programming, John McCarthy's LISP (1958 to 1960) and ALGOL 60 made recursive procedures a first-class language feature. The Tower of Hanoi puzzle was published by Édouard Lucas in 1883.

---

## Compass

**Roots** — *where this comes from*
Every recursive call pushes a frame, which is why recursion is really a story about [[Stack vs Heap Memory|the call stack]] and why the explicit [[Stack and Queue|stack data structure]] can always replace it.

**Paths** — *where this leads*
Tree recursion recomputes the same subproblems over and over, and caching those answers is exactly what turns it into [[Dynamic Programming]]. It is also how depth-first traversal is usually written in [[Breadth-First and Depth-First Search]].

**Neighbors** — *what lives nearby*
Traversals of a [[Binary Search Tree]] and reversing a [[Linked List]] are the textbook recursive exercises, and merge sort and quicksort in [[Sorting Algorithms]] are recursion applied as divide and conquer.

**Clash** — *what pushes against this*
Deep recursion can blow the stack on inputs a loop would handle easily, and Python caps recursion depth at about a thousand by default. When the recursion tree branches, its cost is exponential in [[Big-O Notation]] unless you memoise.
