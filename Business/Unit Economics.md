---
type: atomic
tags: [business/strategy, ai/llm, framework]
date: 2026-10-04
---

# Unit Economics

## Idea
Know what one unit of value costs you to deliver, then model that cost at your expected load and at ten times it.

## Definition
**Unit economics** asks what it costs to produce one unit of the thing a customer actually values (one report, one critique, one active user-month) and compares it to what that unit earns. Totals hide this; a monthly bill tells you nothing about whether growth helps or hurts. For AI products the answer is often surprising. A worked example: a small tool that generates one AI critique per request cost about $0.07 to $0.10 per critique. At three users that came to roughly $10 to $20 a month, but at thirty users it was around $125 to $175. Hosting barely moved; the **LLM API calls dominated** the bill. That changes where optimisation effort goes, toward fewer or cheaper model calls rather than smaller servers. The habit worth keeping is to compute the cost per unit, then project it at expected load and at **10x**, because a cost that is trivial today can be the business model's breaking point at modest scale.

## Source
The concept comes from management accounting (contribution margin per unit). It became startup vocabulary through SaaS metrics, notably David Skok's "SaaS Metrics" writing at Matrix Partners (around 2010), which framed viability as customer lifetime value against acquisition cost with a 3:1 rule of thumb.

---

## Compass

**Roots** — *where this comes from*
It is the money side of [[Scalability-and-Load-Parameters]]: you can't reason about cost at scale without first naming the load parameter that drives it.

**Paths** — *where this leads*
When the model API dominates, the levers are [[Selective LLM Usage]] and [[Model Tiering]], routing only the hard cases to the expensive model. When hosting dominates, [[Scale-to-Zero]] is the lever instead.

**Neighbors** — *what lives nearby*
[[Assumption Register]] supplies the volume guesses this calculation depends on, and [[Tier-Gated Features]] is one way to price so the unit stays profitable.

**Clash** — *what pushes against this*
Early on, obsessing over per-unit cost can be a distraction from finding anyone who wants the unit at all. [[You Don't Need Money to Make Money]] leans toward building first and optimising later.
