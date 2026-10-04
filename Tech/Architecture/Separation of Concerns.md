---
type: atomic
tags: [coding/architecture, coding/patterns, mental-model]
date: 2026-10-04
---

# Separation of Concerns

## Idea
Split a program so that each part deals with one aspect of the problem and can be understood, changed and reused without thinking about the others.

## Definition
A **concern** is one aspect of what the software must do: fetching data, deciding what it means, formatting it, writing it somewhere, handling errors. **Separation of concerns** means each piece of code focuses on one of these, and the boundaries between them are explicit. The most useful everyday split is between **computing** and **doing I/O**. A formatter that turns a transcript into a note should *return a string*, and let its caller decide whether that string goes to a file, a clipboard or a network request. This seems minor until a second use case arrives. When a new capture path was added (say, recording from a phone instead of a desktop), the existing transcriber and formatter were reused unchanged; only a new thin caller was written, because neither module had ever assumed where its input came from or where its output went. Mixed concerns produce the opposite: a function that formats *and* writes to disk can't be reused for anything that doesn't want a disk file, and can't be tested without one.

## Source
Coined by Edsger W. Dijkstra in "On the role of scientific thought" (EWD447, 30 August 1974), where he describes "the separation of concerns" as the only available technique for effective ordering of one's thoughts. Published in his *Selected Writings on Computing: A Personal Perspective* (Springer, 1982).

---

## Compass

**Roots** — *where this comes from*
At the level of a single method it is [[One Method One Responsibility]], and at the level of a system it is the reasoning behind layered designs like [[Clean Architecture]].

**Paths** — *where this leads*
Separating computing from I/O leads directly to [[Functional Core, Imperative Shell]] and to code built from [[Pure Functions]] that can be tested in isolation.

**Neighbors** — *what lives nearby*
[[Ports and Adapters]] separates the application from the technologies it talks to, and [[Separation of Duties]] is the same instinct applied to people and permissions rather than code.

**Clash** — *what pushes against this*
Splitting too finely scatters one simple feature across many files, so reading it means jumping everywhere. Some concerns, like logging, security or transactions, cut across everything and refuse to live in one place, which is why tools like [[Middleware]] exist.
