---
type: atomic
tags: [coding/architecture, framework, ai/agents]
date: 2026-10-04
---

# Ubiquitous Language

## Idea
Agree on one precise vocabulary for the problem domain and use it everywhere: in conversation, in docs, in code names. If people and code use different words for the same thing, misunderstandings become bugs.

## Definition
A **ubiquitous language** is a shared set of terms, each with a single agreed meaning, used by everyone working on a system. When a term means two things, you split it into two terms; when two terms mean one thing, you drop one. The language then shows up directly in class names, function names and database tables, so reading the code feels like reading the domain. A practical way to keep it alive is a short **glossary file** in the repository, maintained as the system changes. It works best with a **module map**: for each module, what it owns and, just as important, what it does *not* own. That last part stops responsibilities from quietly leaking between modules. The glossary complements decision records: **decision records explain why** something was chosen at a point in time, while **the glossary says what is true now**. This matters even more when AI coding agents work in the codebase. An agent that reads the glossary first uses the same names as the humans, puts new code in the module that owns it, and doesn't invent a third word for an existing concept.

## Source
Coined by Eric Evans in *Domain-Driven Design: Tackling Complexity in the Heart of Software* (Addison-Wesley, 2003), where it is a core practice alongside bounded contexts, the boundaries within which a given language stays consistent.

---

## Compass

**Roots** — *where this comes from*
It comes from domain-driven design and complements [[Architecture Decision Records (ADR)]]: the records keep the history of why, the language keeps the present tense of what.

**Paths** — *where this leads*
A glossary that falls behind the code is a case of [[Documentation Drift]], and a vocabulary shared through code itself can be enforced by a [[Shared Contract Package]].

**Neighbors** — *what lives nearby*
[[Clarity In, Clarity Out]] applies the same idea to prompts: precise words in, precise work out. [[Spec-Driven Development]] depends on specs and code naming things the same way.

**Clash** — *what pushes against this*
One language rarely stretches across a whole organisation, since "customer" means something different to billing and to support. That is why Evans pairs it with bounded contexts, and why forcing a single global glossary can create its own [[Single Source of Truth]] fights.
