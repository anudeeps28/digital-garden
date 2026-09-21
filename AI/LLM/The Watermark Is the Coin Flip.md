---
type: atomic
tags: [ai/llm, ai/safety, ai/detection]
date: 2026-09-21
---

# The Watermark Is the Coin Flip

## Idea
Generative text watermarking adds nothing to the text; it replaces the model's random choice between equally good next words with a choice driven by a secret key.

## Definition
When a language model picks the next token, there are often several candidates that fit almost equally well ("grey" vs "overcast"). Unwatermarked, the model effectively flips a coin. A sampling-level watermark seeds that coin with a secret key, so the model's tie-breaks follow a pattern that reads as random to anyone without the key but is statistically detectable to anyone with it. No hidden characters, no appended tag, and no information about the user is embedded. The scheme can only answer "does this text carry the pattern?" It cannot say whether a model wrote all of it or merely edited it, and heavy human editing erodes the signal.

## Source
Anthropic's August 2026 announcement that Claude will watermark generated text, following the EU Code of Practice on transparency. The technique descends from Kirchenbauer et al., "A Watermark for Large Language Models" (2023), which introduced "green list" token biasing, and from Google DeepMind's SynthID-Text (2024), the production approach Anthropic adopted.

---

## Compass

**Roots** — *where this comes from*
It exists because sampling in an [[LLM (Large Language Model)]] already involves choosing among near-equivalent [[Tokens]], and any choice that is arbitrary can be made to carry a signal without changing meaning.

**Paths** — *where this leads*
Detection becomes a statistical claim rather than a certainty, which means it will be misused as proof of authorship it was never built to establish, a pattern that feeds [[Dead Internet Theory]] anxieties in both directions.

**Neighbors** — *what lives nearby*
It resembles seeded shuffle on a playlist: the same songs in an order that feels random but was written down in advance. It sits alongside [[Confidence Score]] as another case where a probabilistic signal gets read as a binary verdict.

**Clash** — *what pushes against this*
The watermark only survives while Anthropic's key stays private and the text stays mostly unedited, and it says nothing about text from [[Open Weights vs Closed Models]] that anyone can run without watermarking at all.
