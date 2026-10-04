---
type: atomic
tags: [frontend, web, framework]
date: 2026-10-04
---

# Design Tokens

## Idea
Design tokens are named design decisions (colours, spacing, type sizes, radii) stored as data, so one change updates every screen and platform.

## Definition
A design token gives a name to a raw value, like `color.accent = #E4572E` or `space.md = 16px`, and code refers only to the name. Good systems layer them: **primitive** tokens hold the palette, **semantic** tokens say what a value is for (`color.text.muted`, `color.surface.raised`), and components use only semantic ones. That indirection is what makes theming cheap: a dark mode or a new brand is a different token set, not a code change. A vivid demonstration: three visual prototypes of the same app differed only in their token block, and comparing them side by side was a matter of swapping one file. Tokens are also where **rules** live, for example "one accent colour, used sparingly, only for the primary action", which keeps a design coherent as more people touch it. Tokens are usually written once in JSON and compiled into CSS custom properties, iOS and Android formats.

## Tools
- **Style Dictionary** — Amazon's build tool that turns token JSON into platform outputs.
- **Tokens Studio** — Figma plugin for managing tokens alongside designs.
- **CSS custom properties** — the usual runtime form on the web.

## Source
Coined around 2014 by Jina Anne and Jon Levine on Salesforce's Lightning Design System team. The W3C Design Tokens Community Group (formed 2019) published the first stable Design Tokens Format specification in October 2025.

---

## Compass

**Roots** — *where this comes from*
It applies [[Single Source of Truth]] to visual design: a value is decided in exactly one place and everything else points at it.

**Paths** — *where this leads*
Once decisions are data, a [[Fitness Functions|fitness function]] can fail the build when someone hard-codes a hex colour, and [[Approve the Foundation Before Polish]] suggests settling tokens before styling individual screens.

**Neighbors** — *what lives nearby*
A [[Shared Contract Package]] does for API types what a token package does for design, and component libraries in [[React]] or [[Angular]] are the main consumers.

**Clash** — *what pushes against this*
Too many tokens become their own maintenance burden and [[Documentation Drift]] sets in when names stop matching usage. Taste still matters: tokens make a design consistent, not good, which is where [[Taste Is Earned Conviction]] comes in.
