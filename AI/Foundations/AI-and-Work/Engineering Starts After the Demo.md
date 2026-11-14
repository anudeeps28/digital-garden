---
type: atomic
tags: [ai/work, tech/engineering, vibe-coding]
date: 2026-11-14
---

# Engineering Starts After the Demo

## Idea
Vibe coding gets you a working demo in thirty minutes; engineers are hired for everything that comes after.

## Definition
AI can now take an idea to a running app in half an hour, a job that used to mean two years of learning to code or three months of paying someone. That first stretch is the honeymoon period: everything works, because nothing has been asked of it yet. Then come real users, real data, security, scaling, edge cases, and changes that break what worked yesterday. Vibe-coded apps tend to work fine and then break later, because it is so easy to never look at the backend. For a hobby project that's fine. For anything serious, the engineering starts where the demo ends: architecture, security, reliability, and the long tail that takes most of the time.

## Source
Captured from my own reel on the role of a software engineer now that AI is coding (October 2026).

"Vibe coding" was coined by Andrej Karpathy in a post on X on 2 February 2025 ("fully give in to the vibes… forget that the code even exists"), and was Collins Dictionary's Word of the Year for 2025. The shape of the problem is the much older **ninety-ninety rule**, attributed to Tom Cargill of Bell Labs and popularised by Jon Bentley's *Programming Pearls* column (1985): "The first 90 percent of the code accounts for the first 90 percent of the development time. The remaining 10 percent of the code accounts for the other 90 percent."

---

## Compass

**Roots** — *where this comes from*
It follows from [[First Make It Work, Then Make It Better]]: AI made the "make it work" half nearly free, which shows how big the "make it better" half always was. The qualities that half has to deliver are listed in [[Maintainability-Operability-Simplicity-Evolvability]].

**Paths** — *where this leads*
The after-the-demo work is concrete: [[Design Every UI State]], [[Make Every Deploy Reversible]], [[Authorization]], [[Idempotency]]. It is also the territory where [[The Agents Speak the Spanish]] says the real decisions now sit.

**Neighbors** — *what lives nearby*
It sits beside [[It Works on My Machine]], the classic version of a demo mistaken for a product, and [[Definition of Done]], which is how a team writes down where the demo ends and the product begins.

**Clash** — *what pushes against this*
The line keeps moving. As agents get better at tests, security review and refactoring, more of the "after" gets automated too, and the honeymoon period stretches. What stays is judgment about what *should* be built and how much risk is acceptable. Lines of backend code are not the point.
