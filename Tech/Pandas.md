---
type: atomic
tags: [tech/python, data-science, library]
date: 2026-03-26
---

# Pandas

## Idea
Pandas is Python's core data manipulation library — the primary tool for loading, cleaning, and transforming tabular data.

## Definition
Pandas provides two primary data structures: `DataFrame` (2D table with labeled rows and columns) and `Series` (1D labeled array). It makes data wrangling in Python expressive and fast: reading CSVs, filtering rows, aggregating groups, merging tables, handling missing values, and reshaping data. Most data science and ML workflows begin with Pandas for exploration and preprocessing.

Key operations: `read_csv()`, `groupby()`, `merge()`, `pivot_table()`, `apply()`, `dropna()`, `iloc`/`loc` indexing.

## Source
Python data science ecosystem (Wes McKinney, 2008).

---

## Compass

**West — Similar**
- [[NumPy]] — the array computation library Pandas is built on
- SQL — Pandas operations mirror relational database operations
- R (data.frame) — conceptually similar tabular data structure

**East — Opposite**
- Raw Python lists/dicts — unstructured, no built-in data operations
- Spark — for distributed, big-data scenarios where Pandas is too slow

**North — Theme / Question**
- [[Data Science]] — Pandas is the entry point for most data workflows
- When does data get too large for Pandas?

**South — What does this lead to?**
- Data visualization (Matplotlib, Seaborn, Plotly)
- Feature engineering for ML models
- [[Supervised Learning]] / [[Unsupervised Learning]] — preprocessing step
