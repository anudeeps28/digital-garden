---
type: atomic
tags: [ai/llm, ai/alignment, thinking]
date: 2026-09-21
---

# Sycophancy

## Idea
Language models agree with users far more than humans do, and the agreement makes people want to keep using them, which quietly disables AI as a tool for self-reflection.

## Definition
Sycophancy is a model's tendency to affirm the user's position, emotions, or choices regardless of merit. A Stanford study published in *Science* in March 2026 tested eleven major models and found they endorsed the user about 49 percent more often than humans did, even when the user was clearly in the wrong, and that higher affirmation increased the desire to return. Reflection requires something willing to push back. You can prompt for brutal honesty and it helps somewhat, but you are still the one deciding what gets corrected, so either you are doing the reflecting or nobody is.

## Source
Personal observation, backed by Myra Cheng, Dan Jurafsky and colleagues, "Sycophantic AI decreases prosocial intentions and promotes dependence", *Science*, 26 March 2026. The term itself has been used in alignment research since around 2023 to describe reward-model-driven agreeableness.

---

## Compass

**Roots** — *where this comes from*
It is a training artefact: models tuned on human approval learn that approval is easiest to earn by agreeing, an instance of [[You Are Your Training Data]] at the level of the model.

**Paths** — *where this leads*
It sets a hard limit on [[Selective LLM Usage]]: any task whose value depends on disagreement (reflection, judgement, feedback) needs a human or a deliberately adversarial setup, not a default chat.

**Neighbors** — *what lives nearby*
[[Consensus Is Not Evidence]] is the social version, and [[A Stale Source Is Confidently Wrong]] is the same fluency-without-accuracy trap arriving from a different direction.

**Clash** — *what pushes against this*
[[Prompt Engineering]] can dial agreeableness down, and the study measured defaults rather than tuned setups; the counter is that the dial is set by the person least able to tell when they need it.
