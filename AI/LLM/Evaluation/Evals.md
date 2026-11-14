---
aliases: ["ai/llm/evals"]
type: atomic
tags: [ai/llm, testing, framework]
date: 2026-11-04
---

# Evals

## Idea
Evals are the test suite for an AI feature: a fixed set of inputs with a way to judge the outputs, run before every prompt or model change ships.

## Definition
An eval is a curated set of real-looking inputs paired with a way to score what the model returns. The scorer can be an exact check (did it return valid JSON, did it call the right tool), a reference answer, a rubric scored by another model, or a person. Because LLM output is non-deterministic and has no simple pass/fail, evals replace "it looked fine when I tried it" with a number you can compare across versions. **A prompt change without an eval run is an untested deploy.** The useful ones start small (twenty to fifty cases pulled from real failures), grow every time a new failure shows up in production, and get run the same way every time so a score drop actually means something.

## Source
Popularised by OpenAI's open-source *Evals* framework (2023) and Hamel Husain's essay "Your AI Product Needs Evals" (2024); now standard practice across AI engineering and part of the [[AI Engineer Roadmap]].

---

## Compass

**Roots** — *where this comes from*
Evals are [[Unit Tests]] rebuilt for software whose output is fuzzy, and they answer the same question a [[Definition of Done]] does for a feature with no easy [[Test Oracle]].

**Paths** — *where this leads*
A working eval set is what makes it safe to swap or upgrade models under [[Model Tiering]] or to move off a [[Pin the Model Version|pinned version]], and it is the safety net that lets prompts be versioned and changed like code.

**Neighbors** — *what lives nearby*
[[LLM-as-a-Judge]] is the most common scorer for open-ended answers, and [[Structured Output Validation]] covers the cheap, deterministic checks that should run first.

**Clash** — *what pushes against this*
An eval set can become the target instead of the measure, which is [[Goodhart's Law]] in action, and a model grading a model risks the bias warned about in [[Never Grade Your Own Homework]].
