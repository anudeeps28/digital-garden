---
type: atomic
tags: [tech/frontend, ux, framework]
date: 2026-11-04
---

# Design Every UI State

## Idea
Every screen has five states (ideal, empty, loading, partial and error), and designing only the ideal one leaves users stuck in the other four.

## Definition
Mockups almost always show a screen full of perfect data, but users spend a surprising amount of time somewhere else: the **empty** state before they've added anything, the **loading** state while data arrives, the **partial** state with one item where you planned for fifty, and the **error** state when something fails. Each needs a deliberate design. An empty state should explain what goes here and offer the first action. A loading state should show progress or a skeleton rather than a blank page. An error state should say what happened and what to do next, in plain words. **A new user's first screen is usually the empty state**, so it does more onboarding than any tutorial.

## Source
Scott Hurff's "The UI Stack" (2015), which named the five states (ideal, empty, error, partial, loading); the same idea runs through most design-system guidance on empty states and error messages.

---

## Compass

**Roots** — *where this comes from*
It's frontend design applied to the [[Product Build Checklist]], and the same thinking as [[Graceful Degradation]]: plan for the path where things are missing or broken, not just the happy one.

**Paths** — *where this leads*
Good loading states lead naturally to [[Optimistic UI]] and the [[App Shell]] pattern, and well-designed empty states become the onboarding for the first five minutes of a product.

**Neighbors** — *what lives nearby*
It is the UI version of avoiding a [[Silent Failure]]: an error state that says nothing is just as bad as a backend that swallows an exception.

**Clash** — *what pushes against this*
Designing five states per screen is real extra work, and [[First Make It Work, Then Make It Better]] argues for shipping the ideal state first. The way out is to cover empty and error states in v1 and polish the rest later.
