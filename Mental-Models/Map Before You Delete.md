---
type: atomic
tags: [mental-model, frontend, coding/patterns]
date: 2026-10-04
---

# Map Before You Delete

## Idea
Before removing something, list everything it does and give each item a named new home. Only then delete it.

## Definition
Redesigns and refactors fail less often from what they add than from what they quietly drop. A screen, module, or step usually carries jobs nobody remembers until they're gone: an export button, a keyboard shortcut, an edge-case warning. **Mapping before deleting** makes the inventory explicit. Write down every action or responsibility the thing performs, then beside each one write where it will live afterwards, or a deliberate decision to drop it. A worked example: a redesign planned to remove a settings screen. Before touching it, all twelve of its actions were listed and each was assigned to a specific, named location in the new design. The screen was deleted with zero functionality lost, and the mapping table doubled as the release note.

## Source
G. K. Chesterton's "fence" passage in *The Thing* (1929): a reformer who sees no use for a fence should not be allowed to clear it away until he goes and finds out why it was put there. The mapping table is the practical, software-shaped version of finding out.

---

## Compass

**Roots** — *where this comes from*
It is [[Kaizen]] done safely: improvement by small steps works only if each step doesn't lose ground the last one gained.

**Paths** — *where this leads*
A complete map is the input to [[Separation of Concerns]], since listing what a thing does often reveals that it was doing too many jobs. It also shrinks the [[Blast Radius]] of a removal from unknown to listed.

**Neighbors** — *what lives nearby*
[[Define Contract Before Implementation]] writes down what a thing must do before it exists, and this writes it down before it stops existing. [[Rollback Scripts]] cover the case where the map was incomplete anyway.

**Clash** — *what pushes against this*
Mapping assumes every existing behaviour deserves a home, and some don't. Treating every old feature as sacred is how products accrete clutter; sometimes the right entry in the table is simply "removed on purpose".
