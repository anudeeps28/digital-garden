---
type: atomic
tags: [ai/ml, machine-learning, algorithms]
date: 2026-03-26
---

# Supervised Learning

## Idea
Train a model on labeled examples so it learns to map inputs to correct outputs for new, unseen data.

## Definition
In supervised learning, a model is trained on a dataset where each input has a known, correct output (label). The model learns a function that maps inputs to outputs by minimizing prediction error on the training data. At inference time, it applies this learned function to new inputs. Classic examples: spam classification (input = email, label = spam/not spam), house price prediction (input = features, label = price), image recognition (input = image, label = object class).

Key distinction: the "supervision" refers to the labeled training signal — a human or process has already provided the correct answers the model is learning from.

## Source
Foundational concept in machine learning.

---

## Compass

**West — Similar**
- [[Unsupervised Learning]] — learning patterns without labeled data
- [[Reinforcement Learning]] — learning from reward signals rather than labels

**East — Opposite**
- [[Unsupervised Learning]] — no labels provided; model finds structure itself

**North — Theme / Question**
- [[Machine Learning]] — the broader field of which supervised learning is a core paradigm
- What happens when labeled data is scarce or expensive?

**South — What does this lead to?**
- Classification and regression algorithms — the two main supervised tasks
- [[Neural Networks]] — the dominant model architecture for supervised learning at scale
