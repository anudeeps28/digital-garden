---
type: atomic
tags: [mental-model, systems-thinking, metrics, incentives]
date: 2026-10-25
---

# Goodhart's Law

## Idea
When a measure becomes a target, it stops being a good measure, because people start optimizing the number instead of the thing it was meant to track.

## Definition
A metric is useful because it correlates with something you care about. Make it a target with rewards attached, and people find ways to move the number that don't move the thing. Call centers measured on call length rush customers off the phone. Teams measured on story points inflate their estimates. Students taught to the test learn test-taking. An AI model rewarded on a proxy finds the loophole. The metric wasn't wrong. Pressure broke the correlation it relied on. The more a metric is worth to the people being measured, the faster it decays. Practical defenses: track several metrics that pull against each other, keep the real goal stated next to the number, and retire a metric once it's being gamed.

## Source
Economist Charles Goodhart, in a 1975 paper on UK monetary policy: "Any observed statistical regularity will tend to collapse once pressure is placed upon it for control purposes." The popular wording, "When a measure becomes a target, it ceases to be a good measure," is anthropologist Marilyn Strathern's paraphrase (1997). Donald Campbell stated a similar law for social indicators in 1976. Meadows describes the system-level version as [[Seeking the Wrong Goal]] in [[Thinking in Systems]].

---

## Compass

**Roots** — *where this comes from*
It is the short form of [[Seeking the Wrong Goal]]: a system steered by a proxy ends up maximizing the proxy. It also follows from [[The Purpose of a System Is What It Does]], because once a number is rewarded, raising that number becomes the system's real purpose.

**Paths** — *where this leads*
Individuals gaming the target is [[Rule Beating]]. The fix is to [[Report the Outcome, Not the Metric]] and to measure as close to the real goal as you can.

**Neighbors** — *what lives nearby*
[[LLM-as-a-Judge]] and [[Never Grade Your Own Homework]] run into it in AI: an optimizer pushed hard against a scorer learns the scorer, not the task. [[Percentile-Based-Performance-Metrics]] is a reminder that even an honest metric only shows what it was built to measure.

**Clash** — *what pushes against this*
Read too broadly, it becomes an excuse never to measure anything. Unmeasured work drifts too, and metrics still help when they're used to start a conversation rather than to hand out rewards.
