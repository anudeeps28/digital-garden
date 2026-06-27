---
type: atomic
tags: [ai/llm]
date: 2026-03-24
---

# Tokens

## Idea
A token is the unit an AI reads text in — roughly one word equals one token — and it directly affects cost and context limits.

## Definition
[[LLM (Large Language Model)|LLMs]] don't process text character by character — they break it into tokens (subword pieces). "Hello world" is 2 tokens, but "unbelievable" might be split into "un", "believ", "able" (3 tokens). Every API call to [[Azure OpenAI]] is billed by tokens: input tokens (your [[Prompt Engineering|prompt]] + context) plus output tokens (the model's response). Models also have a maximum context window measured in tokens (e.g., 128K tokens for GPT-4o). This is why [[Chunking]] matters — you can't feed an entire document if it exceeds the token limit, and more tokens = higher cost.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
Text can be measured at different granularities: [[Characters]] are a simpler unit, while [[Words]] are roughly equivalent to tokens (averaging around 1 word ≈ 1.3 tokens).

**Clash** — *what pushes against this*
This token-based billing model contrasts with [[Flat-Rate Pricing]], which charges a fixed price regardless of usage, and the hypothetical [[Unlimited Context]] model that would have no token limits at all.

**Roots** — *where this comes from*
Tokens are the fundamental unit for how [[LLM (Large Language Model)]] measure and process text, and this measurement directly drives the billing structure of services like [[Azure OpenAI]].

**Paths** — *where this leads*
Understanding tokens leads directly to practical applications: [[Chunking]] strategies must respect token limits, [[Prompt Engineering]] effectiveness depends on managing prompt length in tokens, and [[Cost Optimization]] efforts focus on minimizing token consumption to reduce API costs.
