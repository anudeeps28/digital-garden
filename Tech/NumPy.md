---
type: atomic
tags: [tech/python, data-science, library, numerical-computing]
date: 2026-03-26
---

# NumPy

## Idea
NumPy provides fast, multi-dimensional array computation in Python — the numerical foundation of the entire data science stack.

## Definition
NumPy (Numerical Python) introduces the `ndarray` — a fast, memory-efficient N-dimensional array. Unlike Python lists, NumPy arrays store homogeneous data types and support vectorized operations (element-wise math, broadcasting) without explicit loops, making computation orders of magnitude faster. Nearly every scientific Python library (Pandas, SciPy, scikit-learn, TensorFlow, PyTorch) is built on top of NumPy arrays or its conventions.

Key concepts: array creation (`np.array`, `np.zeros`, `np.random`), indexing/slicing, broadcasting, linear algebra (`np.linalg`), and universal functions (ufuncs).

## Source
Python scientific computing ecosystem (Travis Oliphant, 2005).

---

## Compass

**West — Similar**
- [[Pandas]] — tabular data layer built on NumPy
- MATLAB — the numerical computing environment NumPy replaced for many
- PyTorch/TensorFlow tensors — GPU-accelerated analogues

**East — Opposite**
- Python lists — flexible but slow for numerical computation

**North — Theme / Question**
- [[Data Science]] — why is vectorized computation so much faster than loops?
- How does NumPy's memory model differ from Python's?

**South — What does this lead to?**
- [[Pandas]] — tabular data manipulation
- Scientific computing (SciPy, scikit-learn)
- Deep learning frameworks — tensors are NumPy-like arrays on GPUs
