---
type: atomic
tags: [ai/ml, ai]
date: 2026-10-04
---

# Principal Component Analysis

## Idea
PCA finds the few directions along which your data varies most, and re-describes every point using just those directions. You keep most of the information in far fewer numbers.

## Definition
Given data with many features, **principal component analysis** first centres it (subtracts the mean of each feature), then finds a new set of orthogonal axes called **principal components**. The first component is the direction of maximum **variance**; the second is the direction of maximum remaining variance at right angles to the first, and so on. Mathematically they are the **eigenvectors of the covariance matrix**, ordered by their **eigenvalues**, which measure how much variance each captures; in practice it is computed with a singular value decomposition. Projecting onto the top k components gives a k-dimensional version of the data. Keeping enough components to explain, say, 95% of the variance often cuts hundreds of features down to tens. Uses include visualising high-dimensional data in 2D, removing correlated features before training, compressing images (the classic "eigenfaces"), and denoising, since small-variance directions are often mostly noise. Features must be on comparable scales first, or the one measured in the largest units dominates.

```python
from sklearn.decomposition import PCA
X2 = PCA(n_components=2).fit_transform(X)
```

## Source
Karl Pearson, "On Lines and Planes of Closest Fit to Systems of Points in Space" (Philosophical Magazine, 1901), described it geometrically; Harold Hotelling developed the algebraic formulation and the name "principal components" in 1933.

---

## Compass

**Roots** — *where this comes from*
It is a core method of [[Unsupervised Learning]], needing no labels at all, and it is a few lines of linear algebra in [[NumPy]].

**Paths** — *where this leads*
Reducing a [[Vector Embedding]] to two components is the usual way to plot embeddings and see whether similar items really cluster.

**Neighbors** — *what lives nearby*
A [[Convolutional Neural Network]] also learns compact features from raw data, but nonlinear ones learned for a task, where PCA's are linear and task-blind.

**Clash** — *what pushes against this*
Maximum variance is not maximum usefulness: the direction that separates two classes can have small variance and be thrown away, and nonlinear structure needs methods like t-SNE, UMAP or autoencoders.
