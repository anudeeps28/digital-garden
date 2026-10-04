---
type: atomic
tags: [coding/kotlin, frontend]
date: 2026-10-04
---

# Kotlin

## Idea
Kotlin is a concise, null-safe language on the JVM that became the default way to build Android apps. Its standard tools push you toward immutable data and a single source of UI state.

## Definition
**Kotlin** compiles to JVM bytecode (and also to JavaScript and native code) and interoperates fully with Java. Several features shape how code is written. **Null safety** is in the type system: `String` can never be null, `String?` can, and the compiler forces you to handle the null case with `?.`, `?:` or an explicit check. **Data classes** generate `equals`, `hashCode`, `toString` and **`copy()`**, so updating state means creating a modified copy rather than mutating: `state.copy(isLoading = false)`. `val` is read-only by default. **Coroutines** provide lightweight async code with `suspend` functions, and **Flow** / **StateFlow** expose streams of values that a UI can observe. **Jetpack Compose** builds Android UI declaratively: composable functions describe the screen for a given state, and the framework re-renders when that state changes. The idiomatic architecture holds one immutable UI-state object in a ViewModel, exposes it as a `StateFlow`, and updates it only through events, which is a reducer in everything but name.

## Source
JetBrains announced Project Kotlin in July 2011 (led by Andrey Breslav) and released 1.0 in February 2016. Google added official Android support in 2017 and declared Android "Kotlin-first" at Google I/O 2019. Jetpack Compose reached 1.0 in July 2021.

---

## Compass

**Roots** — *where this comes from*
Immutable data classes and `copy()` encourage [[Pure Functions]] that return new state instead of changing old state.

**Paths** — *where this leads*
A Compose screen fed by one `StateFlow` is the [[Reducer Pattern]] in practice, and the same shape as [[Angular Signals]] or [[React]] state on the web.

**Neighbors** — *what lives nearby*
Coroutines play the role that [[Async Await in CSharp]] plays in .NET, and null-safe types aim at the same bugs as [[TypeScript]] strict mode.

**Clash** — *what pushes against this*
Java interop leaks "platform types" whose nullness the compiler cannot know, and build times and tooling weight remain heavier than in leaner languages.
