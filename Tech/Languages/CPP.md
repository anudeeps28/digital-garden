---
type: atomic
tags: [coding/cpp, coding/embedded]
date: 2026-10-04
---

# CPP

## Idea
C++ is C with abstractions that cost nothing at run time: classes, templates and deterministic destructors on top of direct access to memory and hardware.

## Definition
**C++** is a compiled, statically typed language that keeps C's model of memory and adds tools for building larger systems. **Classes** with constructors and destructors give [[RAII and Smart Pointers|RAII]], the language's central idea for managing resources. **Templates** let you write generic code that the compiler specialises for each type, which is how the **Standard Template Library (STL)** provides containers (`vector`, `map`, `unordered_map`), iterators and algorithms (`sort`, `find`) that are as fast as hand-written versions. The guiding principle is **zero-cost abstraction**: what you do not use, you do not pay for, and what you do use you could not hand-code any better. Modern C++ (C++11 onward) added move semantics, lambdas, `auto`, smart pointers, and later concepts, ranges and modules, so idiomatic code today looks very different from 1990s C++. It dominates where performance and control both matter: game engines, browsers, databases, trading systems, robotics middleware, and increasingly firmware, where a disciplined subset (no exceptions, no heap after startup) runs on microcontrollers.

## Source
Bjarne Stroustrup began "C with Classes" at Bell Labs in 1979; it was renamed C++ in 1983 and released commercially with the first edition of *The C++ Programming Language* in 1985. Standardised as ISO C++98, with major revisions in C++11, C++14, C++17, C++20 and C++23.

---

## Compass

**Roots** — *where this comes from*
It inherits C's direct view of memory, so [[Stack vs Heap Memory]] and [[Memory-Mapped IO]] are everyday concerns rather than hidden details.

**Paths** — *where this leads*
The original [[Design Patterns (Gang of Four)]] were written largely in C++, and the STL's containers are the textbook structures, from [[Hash Table]] to [[Heap and Priority Queue]].

**Neighbors** — *what lives nearby*
[[CSharp]] borrowed much of its syntax while moving to managed memory, and [[Kotlin]] shows a different modern answer to safety through null-aware types.

**Clash** — *what pushes against this*
The language is huge and full of undefined behaviour, and memory-safety bugs are common enough that newer systems languages such as Rust were created largely to remove them.
