---
type: atomic
tags: [business/strategy, framework, workflow]
date: 2026-10-04
---

# Explicit Non-Goals

## Idea
Write down what a product or version will deliberately *not* do, each with its reason, so the scope stays put and the same debate doesn't come back every week.

## Definition
A goals list says where you're going; a **non-goals** list says which reasonable destinations you've chosen to skip. The distinction matters: a non-goal is not a negated goal like "the app shouldn't crash", but something that could sensibly be a goal and was consciously ruled out. In a product requirements document this shows up as a "Non-goals (V1)" section, plus a parking lot of **V2 candidates**, each carrying its cost or reason. A worked example: a small app considered pulling data by scraping a large platform. The idea was parked as a V2 candidate with its reason attached, roughly $50 to $100 a month in scraping infrastructure plus fragility when the platform changes its pages. Months later, when someone suggested it again, the answer was one line in the doc rather than a fresh hour of discussion. The written reason does two jobs: it stops scope creep, and it makes clear what would have to change for the item to be reconsidered.

## Source
Popularised by Google's design-doc culture, where "Goals and non-goals" is a standard early section; Malte Ubl's widely read essay "Design Docs at Google" (2020) defines non-goals as things that could reasonably be goals but are explicitly chosen not to be, giving "ACID compliance" for a database as an example.

---

## Compass

**Roots** — *where this comes from*
It shares its logic with [[Architecture Decision Records (ADR)]]: a decision written with its reason is a decision you don't have to make twice. It also draws on [[Slow Productivity]], which argues that doing fewer things is the precondition for doing them well.

**Paths** — *where this leads*
Non-goals give a [[Definition of Done]] its edges, and parked items with costs attached become a ready-made input to [[Unit Economics]] when version two is planned.

**Neighbors** — *what lives nearby*
[[Record the Reason, Not Just the Blocker]] is the same move applied to unfinished work, and [[JOMO (Joy of Missing Out)]] is its personal-life cousin. [[Grill the Plan]] is often where non-goals are discovered.

**Clash** — *what pushes against this*
A non-goals list can harden into dogma, keeping out the one feature users actually needed. [[Managing Ambiguity]] argues for revisiting scope when evidence changes, so each non-goal should state what would reopen it.
