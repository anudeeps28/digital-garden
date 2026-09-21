---
type: atomic
tags: [coding/architecture, coding/patterns, devops, iac]
date: 2026-09-16
---

# Single Source of Truth

## Idea
The same value written in two places isn't redundancy. It's a bug with a delay fuse — someone will change one of them.

## Definition
Single source of truth means each fact in a system has exactly one authoritative definition, and everything else derives from it by reference rather than by copy. A resource name declared in a template and again in a pipeline variable; a connection string in configuration and in a deployment script; a status enum in the backend and hand-mirrored in the frontend — each of these works perfectly on the day it's written and diverges the first time someone updates one side. The failure is invisible at the moment it's introduced, which is what makes it worth treating as a defect *before* the drift happens rather than after. The remedy is a reference, an import, or a generated artifact, so the second location can't hold a different value. Where duplication is genuinely unavoidable, the fallback is a check that asserts the two agree — see [[Orphan Resource Sweep]].

## Source
A foundational principle in information systems and database normalization; closely related to Don't Repeat Yourself as stated in Hunt and Thomas's *The Pragmatic Programmer* (1999).

---

## Compass

**Roots** — *where this comes from*
The same normalization instinct behind [[Relational Database]] design, applied to configuration and code rather than rows.

**Paths** — *where this leads*
In infrastructure it argues for [[Bicep Parameter File|parameter files]] and outputs over repeated literals; in application code, for generated clients over hand-mirrored types.

**Neighbors** — *what lives nearby*
[[Define Contract Before Implementation]] is the same idea earlier in the lifecycle — establish the one definition before anyone can make a second.

**Clash** — *what pushes against this*
Removing duplication creates coupling. Two independent copies can evolve separately, which is occasionally exactly what you want — and one shared definition can force unrelated components to change together.
