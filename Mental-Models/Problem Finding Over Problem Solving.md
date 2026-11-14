---
type: atomic
tags: [mental-model, ai/agents, creativity]
date: 2026-11-14
---

# Problem Finding Over Problem Solving

## Idea
When solving gets cheap, the human edge moves upstream: choosing which problems are worth solving, and designing the systems that solve them.

## Definition
For centuries, being the one who solved the hard problem was the prize, and people competed for it and fought over the credit. That race is now against something that doesn't eat, doesn't sleep and doesn't want the prize, so racing to be the solver is a losing position. What stays with humans is the earlier part of the work: noticing a problem, framing it so it can be worked on, deciding it matters, and building the harness of specialised agents, checks and verification that gets it solved. A well-framed problem is half solved. A brilliant solution to a badly chosen problem is worth nothing.

## Source
Captured from my own reel on AI agents and an open math problem (October 2026). The news behind it, checked and corrected: on 8 September 2026 OpenAI announced that about 10,000 agents, running for about 88 hours, had produced a Lean-formalised proof of finite-time blowup for the *forced* variants of the Navier–Stokes Millennium Problem. The unforced problem is still open, and the Clay prize has not been awarded. There was a public credit dispute. An NYU mathematician, working with an Anthropic researcher, had posted related Lean-verified blowup results the day before and accused OpenAI of building on their approach; OpenAI denies any access to their draft.

The concept is older. Jacob Getzels and Mihaly Csikszentmihalyi's study of art students, *The Creative Vision* (1976), found that the students who spent the most time *finding and framing* the problem produced the most original work and had the most successful careers. Einstein and Infeld, in *The Evolution of Physics* (1938), put it this way: "The formulation of a problem is often more essential than its solution."

---

## Compass

**Roots** — *where this comes from*
This is [[Tie Your Identity to How You Think]] at its sharpest: the one judgment that is hardest to automate is which problem deserves the effort. It also follows from [[Depth Is Cheap]], because once solving depth can be borrowed, what is scarce is knowing where to aim it.

**Paths** — *where this leads*
In practice, problem finding becomes harness design. The [[Agent Harness]] and the [[Orchestrator-Subagent Pattern]] are how a framed problem gets turned into work thousands of agents can do, and [[Evals]] are how you know they solved the problem you actually framed.

**Neighbors** — *what lives nearby*
It sits near [[Direct and Check]], which is problem finding at the scale of one task, and near [[Zero-Sum vs Positive-Sum Games]], because a fight over credit is a zero-sum game being played inside a positive-sum one.

**Clash** — *what pushes against this*
You can't frame problems well in a field you have never solved problems in; taste comes from doing the work, as [[Taste Is Earned Conviction]] argues. The credit dispute in the source also shows that "the humans just pick problems" undersells how much human work fed the solve.
