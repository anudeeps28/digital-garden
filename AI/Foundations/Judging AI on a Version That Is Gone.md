---
type: atomic
tags: [ai/llm, ai/agents, mental-model]
date: 2026-09-21
---

# Judging AI on a Version That Is Gone

## Idea
Most people's picture of what AI can do is a year old, and the gap between that picture and the current frontier is where the useful work is.

## Definition
If the last time you tried a frontier model was a year ago, you are working from a stale picture. Three probes reveal the gap. Hand a model a whole project and ask for an audit, or give it a bug nobody has explained. Ask it to build you an agent, since the assumption that agents are hard and unreliable has stopped being true. Tell it the hardest unsolved problem in your work, and stay for the conversation, because it will ask questions before it answers. Each probe tests something an older model could not do, which is the point.

## Source
Personal reflection around the September 2026 releases of Claude Fable 5.1 and GPT-6 Astra. Anthropic's announcement included Millennium's account of a one-in-a-million crash, unexplained for four years, that Fable 5.1 traced to a vendor library by disassembling it against a core dump after every prior model had missed it.

---

## Compass

**Roots** — *where this comes from*
It is [[A Stale Source Is Confidently Wrong]] applied to your own memory: the old verdict answers fluently and gives no sign it is out of date.

**Paths** — *where this leads*
The second probe leads into agent building, which needs [[n8n Orchestrates AI Reasons]] style thinking about harnesses rather than prompts, and the third leads into using the model as a sparring partner rather than an oracle.

**Neighbors** — *what lives nearby*
[[Learning Agility]] is the trait being tested: whether you re-examine a tool you already dismissed.

**Clash** — *what pushes against this*
[[Sycophancy]] cuts against the sparring-partner probe, because a model that asks good questions can still tell you what you want to hear once it has the answers.
