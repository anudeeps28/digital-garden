---
type: atomic
tags: [coding/patterns, coding/architecture, coding/cpp]
date: 2026-10-04
---

# Design Patterns (Gang of Four)

## Idea
A design pattern is a named, reusable solution to a problem that keeps recurring in object-oriented code. The real value is the shared vocabulary: saying "use a Strategy here" carries a whole design in two words.

## Definition
The 1994 catalogue describes 23 patterns in three groups. **Creational** patterns control how objects are made: Factory Method, Abstract Factory, Builder, Prototype, Singleton. **Structural** patterns compose objects into larger shapes: Adapter, Decorator, Facade, Proxy, Composite, Bridge, Flyweight. **Behavioral** patterns divide responsibilities and communication: Strategy, Observer, Command, State, Iterator, Template Method, Visitor, Chain of Responsibility, and others. Each entry records intent, structure, participants and consequences, so you learn when *not* to use it as well. Two principles run through the book: "program to an interface, not an implementation" and "favour object composition over class inheritance". Many patterns now ship inside languages and frameworks rather than being hand-written. Observer is what an [[RxJS Observable]] or [[Angular Signals|signal]] gives you for free; a static creation method on an entity is a Factory Method; middleware pipelines are Chain of Responsibility; iterators are built into every modern language.

## Source
Erich Gamma, Richard Helm, Ralph Johnson and John Vlissides, *Design Patterns: Elements of Reusable Object-Oriented Software* (Addison-Wesley, 1994), whose four authors became "the Gang of Four". They credited Christopher Alexander's *A Pattern Language* (1977) in architecture as the inspiration.

---

## Compass

**Roots** — *where this comes from*
The book's examples were written in [[CPP|C++]] and Smalltalk, and the interface-first principle is the same one behind [[Interfaces in CSharp]].

**Paths** — *where this leads*
[[Strategy Pattern]] and [[Dependency Injection]] are the patterns most visible in modern backends, and [[Entity Factory Method]] is a direct descendant of Factory Method.

**Neighbors** — *what lives nearby*
The State pattern is the object form of a [[Finite State Machine]], and Observer distributed over a network becomes the [[Publish-Subscribe Pattern]].

**Clash** — *what pushes against this*
Applied by rote, patterns produce layers of indirection with no problem to solve, and Peter Norvig showed in 1996 that most of the 23 vanish or simplify in languages with first-class functions, which is part of why [[Pure Functions]] often replace them.
