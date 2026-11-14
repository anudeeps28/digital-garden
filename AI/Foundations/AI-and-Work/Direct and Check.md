---
type: atomic
tags: [ai/work, ai/agents, business/career]
date: 2026-11-14
---

# Direct and Check

## Idea
When doing the task gets cheap, the two skills that get expensive are directing the work and checking it.

## Definition
The same tool produces wildly different outcomes depending on the person holding it, and the difference sits at the two ends of the work. **Directing** is deciding what to build, what to fix, what to ship, and steering the tool there. **Checking** is refusing to accept output you have not verified. Someone who does both gets leverage; someone who does neither gets a confident mess with their name on it. Directing without checking ships hallucinations. Checking without directing produces correct answers to the wrong questions. For any task you marked as "AI can do this", stop doing it by hand, and learn to direct it and to check it.

## Source
Captured from my own long-form video on AI and job fear (October 2026). The three cases were checked:

- **Directing:** Pieter Levels, a solo founder who had never made a game, started a browser flight simulator on 22 February 2025. Using Cursor, he had it live in about three hours. He claimed $1M annualised revenue within 17 days (about $87K MRR annualised). That figure is self-reported, and later reports suggest the revenue fell away quickly.
- **Checking:** In *Mata v. Avianca* (S.D.N.Y., June 2023), lawyers filed a brief citing six cases that ChatGPT had invented. When the court questioned them, they stood by the fake opinions. The judge found bad faith and fined them and their firm $5,000.
- **Checking, at scale:** In 2025, Deloitte delivered an A$440K report to Australia's employment department that contained a fabricated quote attributed to a Federal Court judge and references to papers that do not exist. Deloitte repaid the final instalment, which Senate estimates put at A$97,587, under a quarter of the fee.

---

## Compass

**Roots** — *where this comes from*
This is what's left once [[A Job Is a Bundle of Tasks]] has had its cheap task removed. It is also the working form of [[AI as Amplifier]]: the tool amplifies the clarity of your direction and the rigour of your checking, or the lack of both.

**Paths** — *where this leads*
Checking at scale turns into infrastructure: [[Evals]], [[Field Verification]] and the rule that you should [[Never Grade Your Own Homework]]. Directing at scale turns into an [[Agent Harness]], where the steering is written down once instead of repeated in every prompt.

**Neighbors** — *what lives nearby*
It sits beside [[Hand Off the Code, Not the Understanding]], which is the precondition for both halves: you cannot direct a system you do not understand, and you cannot check output you could not have reasoned about yourself.

**Clash** — *what pushes against this*
Checking does not scale linearly. As agents produce more, line-by-line review becomes the bottleneck, which is why [[Validate Before You Automate]] pushes trust into tests and guardrails instead of eyeballs. The Levels story also shows survivorship bias: plenty of well-directed projects never hit a million.
