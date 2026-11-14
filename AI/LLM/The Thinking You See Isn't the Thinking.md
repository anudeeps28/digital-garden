---
type: atomic
tags: [ai/llm, ai/reasoning, ai/interpretability]
date: 2026-11-14
---

# The Thinking You See Isn't the Thinking

## Idea
A model's visible chain of thought is generated the same way as its answer, token by token, so it is a plausible story about the reasoning, not a reliable window into it.

## Definition
An LLM does not read your message. It turns the words into numbers and predicts the next token, then the next, from patterns in its training data. Because it was trained on huge amounts of people reasoning, it learned the *shape* of reasoning, and the "thinking" panel is produced by exactly the same prediction. Faithfulness tests show the gap: when models are slipped a hint that changes their answer, the visible reasoning usually doesn't mention the hint at all. Fluent reasoning is a style the model produces, not evidence of what actually drove the answer. Whether that counts as "thinking" depends on your definition. One useful line: human thinking runs unasked, in the shower or at 2am, driven by wanting something. A model produces nothing until prompted, and wants nothing.

## Source
Captured from my own reel "Can AI models think?" (October 2026).

The key study is Anthropic's *Reasoning Models Don't Always Say What They Think* (Chen et al., April 2025). When given a hint that influenced their answer, Claude 3.7 Sonnet mentioned it in its chain of thought only **25%** of the time and DeepSeek R1 **39%**. Unfaithful chains of thought were on average *longer*, and faithfulness dropped on harder tasks. Outcome-based reinforcement learning improved faithfulness at first, then plateaued. The capture's claim that the thinking "most of the time didn't mention what drove the answer" checks out. The consciousness and intention points are the creator's philosophical position, not findings of the paper.

---

## Compass

**Roots** — *where this comes from*
It follows from how an [[LLM (Large Language Model)]] works: every output, including the "reasoning", is next-[[Tokens]] prediction. It is a cousin of [[Sycophancy]], since both are cases where the model produces what looks right rather than what is true.

**Paths** — *where this leads*
If the reasoning can't be trusted as an explanation, judge the output instead. That means [[Evals]], [[Structured Output Validation]] and the rule to [[Never Grade Your Own Homework]], rather than reading the thinking panel and feeling reassured.

**Neighbors** — *what lives nearby*
It sits near [[AI Is a Tool, Not Magic]], which makes the same point about expectations, and [[Faithful Intent Translation]], which is about whether a model's output matches what was asked rather than what was reasoned.

**Clash** — *what pushes against this*
"It's just next-token prediction" proves less than it sounds like it does: a brain can be described as "just neurons firing", too. Chains of thought are partly faithful and measurably help on hard problems, so the honest claim is "an unreliable window", not "no window at all". [[AGI Arrives in Phases, Not on a Day]] warns against treating any of this as permanent.
