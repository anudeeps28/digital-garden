---
type: atomic
tags: [ai/ml, machine-learning, algorithms]
date: 2026-03-26
---

# Unsupervised Learning

## Idea
Find hidden structure in data without labeled examples — let the model discover patterns on its own.

## Definition
In unsupervised learning, the training data has no labels. The model must find patterns, groupings, or representations by itself. Common tasks: clustering (group similar data points — e.g., customer segmentation), dimensionality reduction (compress data while preserving structure — e.g., PCA, t-SNE), and generative modeling (learn the data distribution to generate new samples — e.g., GANs, VAEs). The challenge: without ground truth, evaluating model quality is harder than in supervised learning.

## Source
Foundational concept in machine learning.

---

## Compass

**West — Similar**
- [[Supervised Learning]] — the labeled counterpart
- Self-supervised learning — a hybrid where labels are generated from the data itself

**East — Opposite**
- [[Supervised Learning]] — has explicit labels and a known target

**North — Theme / Question**
- [[Machine Learning]] — the broader field
- How do we evaluate models when there is no ground truth?

**South — What does this lead to?**
- Clustering algorithms (k-means, DBSCAN)
- Dimensionality reduction (PCA, t-SNE, UMAP)
- [[Generative AI]] — many modern generative models are trained unsupervised or self-supervised
