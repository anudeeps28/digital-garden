---
type: atomic
tags: [ai/agents, ai/llm, mental-model]
date: 2026-10-04
---

# Faithful Intent Translation

## Idea
An AI that relays a person's instruction to another agent may clarify what the person meant, but must never add to it.

## Definition
When one model sits between a human and another agent, such as a voice assistant passing spoken instructions to a coding agent, it is tempting to let it "improve" the request. **Faithful intent translation** draws a hard line. Allowed: resolving references ("that button" becomes the actual component name, "the thing we just changed" becomes the file), fixing transcription slips, and adding context the person clearly pointed at. Not allowed: adding requirements, choosing between options the person left open, or answering the downstream agent's questions on the person's behalf. Everything the relay sends stays visible to the human, so any drift is caught. A practical detail from one such relay: the translating step calls a small model only on demand, when there is actually a reference to resolve; plain instructions pass through untouched.

## Source
No single coined origin; it is a design principle for agent pipelines. The underlying norm echoes Paul Grice's maxim of quantity in "Logic and Conversation" (1975): make your contribution as informative as required, and no more.

---

## Compass

**Roots** — *where this comes from*
The allowed half is [[Co-reference Resolution]] and the [[Follow-Up Rewriter]] from retrieval systems, which rewrite a vague message into a standalone one without changing what is asked.

**Paths** — *where this leads*
Deciding when a translation is even needed is a small [[Query Intent Classification]] problem, which is why a cheap model is enough and [[Model Tiering]] applies.

**Neighbors** — *what lives nearby*
[[Propose, Don't Execute]] sets the same boundary for actions that this sets for words, and [[Clarity In, Clarity Out]] is why the relay must not blur intent.

**Clash** — *what pushes against this*
Strict faithfulness passes the person's vagueness straight through, so sometimes [[Ask It to Ask You]] is better: the relay should ask rather than guess or embellish.
