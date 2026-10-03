---
type: atomic
tags: [ai/ml, learning, framework]
date: 2026-10-03
---

# Learn the Loop, Not the Algorithm

## Idea
The durable skill in machine learning is the cycle — get data, clean it, train something, measure whether it worked, do it again — because the algorithms change every year and the loop doesn't.

## Definition
Beginners treat ML as a catalogue of models to memorise, which is why a year of study can leave someone unable to start a real problem. The actual job is a loop, and almost all of it happens outside the model: finding data, discovering it is dirty, deciding what "worked" even means for this problem, measuring it honestly, and going around again. Someone who has run that loop end-to-end three times on three different kinds of data can pick up an unfamiliar architecture in a week. Someone who has memorised twenty architectures and never closed the loop cannot ship anything. Pick the algorithm for the problem in front of you; the transferable asset is the cycle.

## Source
From the "how to learn machine learning" video (September 2026), which puts one end-to-end scikit-learn project in the first two months specifically to teach the loop rather than any algorithm. The full six-month path is written up as the [[Machine Learning Roadmap]].

The loop is old enough to be a standard: CRISP-DM, developed in 1996, formalises it as business understanding, data understanding, data preparation, modeling, evaluation and deployment, with explicit permission to jump back to any earlier phase. Andrew Ng's version in *Machine Learning Yearning* compresses it to idea → code → experiment, and he attributes most practical progress to shortening the time around that cycle rather than to any single idea within it.

---

## Compass

**Roots** — *where this comes from*
It presumes you have somewhere to apply the loop, which is what [[Supervised Learning]] supplies as the first concrete instance — labelled examples, a prediction, a measurable error. It is the learning-strategy consequence of [[Fun Is Not the Same as Getting Good]], since deriving the maths is the enjoyable part and closing the loop is the part that works.

**Paths** — *where this leads*
Closing the loop honestly forces the question of what you are measuring and for whom, which is where [[Report the Outcome, Not the Metric]] takes over. Repeated enough, it is [[Kaizen]] applied to a model rather than a habit.

**Neighbors** — *what lives nearby*
The same iteration shows up in [[Unsupervised Learning]], where the absence of labels makes the evaluation step harder but no less necessary. It is the ML-shaped instance of [[First Make It Work, Then Make It Better]] — get a bad model end-to-end before improving any single stage of it.

**Clash** — *what pushes against this*
Taken too literally the loop becomes metric-chasing on clean data, which is the specific thing that makes a strong Kaggle finish a weak hiring signal — optimising a number is not shipping. And some problems genuinely are architecture problems, where no amount of looping substitutes for understanding the model; that is the discrimination [[Selective Intelligence]] asks for, knowing when the loop is the answer and when to put it down.
