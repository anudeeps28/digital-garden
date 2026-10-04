---
type: atomic
tags: [coding/cpp, coding/patterns]
date: 2026-10-04
---

# RAII and Smart Pointers

## Idea
Tie every resource to the lifetime of an object: acquire it in the constructor, release it in the destructor. When the object goes out of scope, for any reason including an exception, the cleanup happens on its own.

## Definition
**RAII** (Resource Acquisition Is Initialization) is the core C++ idiom for anything that must be released: memory, file handles, locks, sockets, GPIO claims. Because C++ destructors run deterministically when a stack object leaves its scope, wrapping the resource in a small class guarantees release without a single explicit `free` or `close` in the calling code. `std::lock_guard` releasing a mutex and `std::fstream` closing a file are classic examples. **Smart pointers** apply RAII to heap memory. `std::unique_ptr<T>` is the sole owner: it cannot be copied, only moved, and it deletes the object when it dies, with no runtime cost over a raw pointer. `std::shared_ptr<T>` keeps a reference count and deletes when the last owner goes away. `std::weak_ptr<T>` observes a shared object without keeping it alive, breaking reference cycles that would otherwise leak. The modern rule is that raw `new` and `delete` should almost never appear in application code: use `std::make_unique` and let ownership be visible in the types. C# reaches for the same goal with `IDisposable` and `using`, and Python with `with` blocks, though there it is opt-in rather than built into every object's lifetime.

## Source
Developed by Bjarne Stroustrup and Andrew Koenig during 1984–1989 for exception-safe resource handling; Stroustrup coined the name and described it in *The Design and Evolution of C++* (1994). `auto_ptr` arrived in C++98; `unique_ptr`, `shared_ptr` and `weak_ptr` were standardised in C++11, building on Boost.

---

## Compass

**Roots** — *where this comes from*
It is the answer to the leaks and dangling pointers described in [[Stack vs Heap Memory]], and it only works because [[CPP|C++]] runs destructors at a known moment.

**Paths** — *where this leads*
Explicit ownership in types makes [[Device Driver]] code safer, since a handle that releases the bus on destruction cannot be forgotten on an error path.

**Neighbors** — *what lives nearby*
`using` and `IDisposable` in [[CSharp]] and context managers in [[Python]] are the managed-language cousins.

**Clash** — *what pushes against this*
`shared_ptr` everywhere hides who really owns what and adds atomic reference counting costs, and garbage-collected languages cannot offer the same determinism, so their equivalents depend on the caller remembering to use them.
