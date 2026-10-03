---
type: atomic
tags: [ai/llm, framework, prompt-engineering]
date: 2026-10-03
---

# Ask It to Ask You

## Idea
Instead of trying to write a better prompt, hand the model the job of interrogating you: "ask me five clarifying questions before you answer."

## Definition
A one-line question gets an answer written for the average person asking it, which is why so many people conclude the model is overrated. The fix is context, but supplying context is hard precisely when you don't yet know what matters. Flipping the direction solves that: the model proposes the questions, you supply the specifics, and only then does it answer — now against your actual situation rather than the generic one. It converts the exchange from a search box into a conversation, and it surfaces the variables you would not have thought to mention, which is most of them.

## Source
Captured from my own reel on AI concepts most people miss (September 2026): "ask me five or ten clarifying questions so we have a shared understanding first."

The move has a formal name — the Flipped Interaction Pattern, catalogued in the prompt-pattern literature as the inversion of who drives the exchange. It has since become a research area in its own right: work on teaching models to ask when instructions are under-specified (the "Ask-when-Needed" line of work) and benchmarks like CLAMBER show that models usually *recognise* ambiguity but rarely raise it unprompted — which is exactly why you have to ask them to.

---

## Compass

**Roots** — *where this comes from*
This is an applied corollary of [[Clarity In, Clarity Out]] — output quality tracks input clarity, and the fastest route to a clear input is to let the other party specify what it needs. It is a pattern within the broader craft of [[Prompt Engineering]] rather than a replacement for it.

**Paths** — *where this leads*
Once the clarifying exchange is routine, the answers it produces are worth keeping rather than retyping, which leads toward reusable [[Prompt Pieces]] and, for anything you do repeatedly, [[Turn Repeated Work Into a Skill]].

**Neighbors** — *what lives nearby*
It is the conversational form of [[Define Contract Before Implementation]]: settle what the output must satisfy before anyone starts producing it. It also rhymes with [[Explain in Layers]], in that both treat a mismatch in level as the thing to resolve explicitly rather than guess at.

**Clash** — *what pushes against this*
The weakness is that the questions come from a system with a strong pull toward agreement — [[Sycophancy]] means the model may ask the questions it expects you to enjoy answering, confirming your framing rather than stress-testing it. And the ritual can become its own delay, ten questions deep on something a single sentence would have resolved, which is the misuse [[Selective Intelligence]] warns about.
