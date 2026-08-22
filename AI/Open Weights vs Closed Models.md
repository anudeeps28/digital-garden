---
type: atomic
tags: [ai/llm, open-source, infrastructure, privacy]
date: 2026-08-12
---

# Open Weights vs Closed Models

## Idea
You're either renting someone else's AI brain (closed models) or downloading one to own (open weights) — and most people don't know which they're doing.

## Definition
Closed models (ChatGPT, Claude, Gemini) are brains that live on someone else's servers — they decide when it changes, what it costs, and when it goes away. Your data passes through their infrastructure. Open-weight models give you a file: download the brain, host it yourself, fine-tune it on your own data, make it actually yours. Your data never leaves your machine. Important distinction: open weights ≠ open source — open weights release the model parameters but not necessarily the training code, data, or full architecture. Trade-offs are real: large open-weight models (Kimi K3 at 2.8T parameters) need serious hardware, while smaller ones (Qwen) run on consumer machines but are less capable. And using a model "through their API" means you're renting it regardless of whether the weights are public.

## Source
Anudeep Sharma's content (Instagram, August 2026). The open vs. closed distinction emerged organically in the AI field (2023-2025) as companies like Meta (LLaMA), Mistral, and DeepSeek released model weights while keeping other details proprietary.

---

## Compass

**Roots** — This distinction grows from the broader open-source software movement and connects to [[LLM (Large Language Model)]] architecture — understanding what "weights" are requires knowing how neural networks store learned patterns.

**Paths** — Understanding this distinction enables informed decisions about [[AI Is a Tool, Not Magic]] — knowing whether you own or rent your AI shapes what you can build with it, and connects to privacy and data sovereignty concerns.

**Neighbors** — This lives near [[RAG (Retrieval-Augmented Generation)]] and [[Vector Embedding]] as infrastructure decisions that determine how you build AI systems, and beside the trade-off thinking in [[Selective LLM Usage]].

**Clash** — The "own your model" narrative can be misleading — the weights carry whatever biases were baked into training, guardrails can be fine-tuned off, and self-hosting doesn't automatically mean safer or better, especially without the expertise to evaluate what you're running.
