---
type: atomic
tags: [coding/cpp, coding/embedded]
date: 2026-10-04
---

# Stack vs Heap Memory

## Idea
Local variables live on the stack and disappear automatically when the function returns; anything you allocate on the heap lives until something frees it. Most memory bugs in C and C++ are about getting that second part wrong.

## Definition
The **stack** holds each function call's **frame**: parameters, local variables and the return address. Allocation is just moving a pointer, so it is extremely fast, and cleanup is automatic when the function returns (**automatic storage**). It is also small (often 1 to 8 MB on a desktop thread, a few kilobytes on a microcontroller), so deep [[Recursion]] or a large local array causes a **stack overflow**. The **heap** is a large pool for **dynamic storage**: `malloc`/`free` in C, `new`/`delete` in [[CPP|C++]]. It suits data whose size is known only at run time or that must outlive the function that created it, but every allocation must be released exactly once. Forget, and you have a **memory leak**; free too early and keep using the pointer, and you have a **dangling pointer**; free twice and you corrupt the allocator. Heap allocation is slower and can fragment memory, which is why many embedded and safety-critical projects forbid it after startup. Managed languages such as [[CSharp]] and [[Python]] still use a stack for calls, but put objects on a garbage-collected heap, so leaks become "something still holds a reference" rather than "nobody called free".

## Source
The call stack traces to Bauer and Samelson's stack principle (1957) and ALGOL 60's block-structured locals; Dijkstra's "Recursive Programming" (1960) described the run-time stack implementation. Dynamic allocation through `malloc` was standardised in C (K&R, 1978; ANSI C, 1989).

---

## Compass

**Roots** — *where this comes from*
Every function call pushes a frame on what is literally a [[Stack and Queue|stack]], which is why [[Recursion]] depth is bounded by stack size.

**Paths** — *where this leads*
[[RAII and Smart Pointers]] tie heap lifetimes back to stack lifetimes, turning manual frees into automatic ones.

**Neighbors** — *what lives nearby*
The data structure called a [[Heap and Priority Queue|heap]] shares only the name; the memory heap is a general allocator, not a priority ordering.

**Clash** — *what pushes against this*
Garbage collection removes most of this bookkeeping in exchange for pauses and less predictable memory use, a trade that real-time firmware usually refuses.
