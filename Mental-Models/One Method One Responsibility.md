---
type: atomic
tags: [mental-model, coding/patterns, architecture]
date: 2026-02-23
---

# One Method One Responsibility

## Idea
Each method should do exactly one thing — if you can name a sub-task inside it, that sub-task should be its own method.

## Definition
A method that does one thing is readable (its name tells the whole story), testable (you can test that one thing in isolation), and easy to change (modifying one behaviour doesn't risk breaking another). The signal that a method is doing too much: you find yourself writing an `// and then...` comment inside it, or the method name contains "and". Extract that sub-task into a named private method.

In practice: `Extract()` orchestrates, but delegates to `ExtractSectionHeadings()`, `DetectTableStructures()`, `ComputeStructureHash()` — each doing exactly one thing.

## Source
C# coding session — extractor class design, private helper methods

---

## Compass

**Neighbors** — *what lives nearby*
The [[Single Responsibility Principle (SRP)]] applies this same idea at the class level. [[Define Contract Before Implementation]] pairs naturally with this — a method with one job has a clear contract. [[Guard Clauses]] embody one-thing thinking too, separating validation from logic into distinct concerns.

**Clash** — *what pushes against this*
God functions represent the opposite: one massive method that does everything. The "while I'm in here, I'll also..." mentality creates scope creep at the method level, violating the principle entirely.

**Roots** — *where this comes from*
This traces back to [[Separation of Concerns]], a fundamental architectural principle. The deeper question it answers is: what makes code readable and maintainable? Clean Code explores exactly this.

**Paths** — *where this leads*
Methods that read like English emerge naturally — `ExtractSectionHeadings()` tells you exactly what happens without opening it. This enables easy unit tests, since one responsibility means one behaviour to assert. Safe refactoring follows too: changing one helper method can't break an unrelated one.
