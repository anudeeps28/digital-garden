---
type: atomic
tags: [coding/python]
date: 2026-06-26
---

# PyTorch

## Idea
The deep-learning engine quietly doing the math under our embedding model — and installed lean to keep the image small.

## Definition
PyTorch is a deep-learning framework that provides tensors, automatic differentiation, and the neural-network runtime that models execute on. It serves as the engine beneath higher-level libraries like [[Sentence Transformers]]: when embedding models run (such as all-MiniLM-L6-v2) to turn text into [[Vector Embedding|vectors]], PyTorch is doing the actual forward pass. In practice, developers often install the CPU-only build (no CUDA/GPU stack) deliberately when GPU acceleration is not available, because the CPU wheels make resulting deployments significantly smaller and faster. It's frequently a transitive dependency called indirectly through other libraries rather than invoked directly, but careful attention during build and deployment is important.

## Source
Meta (Facebook AI Research), first released 2016; open-sourced on GitHub. Key paper: Paszke et al., "PyTorch: An Imperative Style, High-Performance Deep Learning Library" in *Advances in Neural Information Processing Systems* (2019).

---

## Compass

**Roots** — *where this comes from*
PyTorch sits within the broader [[Python]] ecosystem and its deep-learning tooling stack.

**Paths** — *where this leads*
The choice between CPU and GPU builds directly affects deployment size and inference latency, and PyTorch's computational output powers the [[Vector Embedding|vectors]] that downstream ML systems consume.

**Neighbors** — *what lives nearby*
[[Sentence Transformers]] is the higher-level library that sits directly on top of PyTorch and provides the embedding functionality we use in practice.

**Clash** — *what pushes against this*
[[Azure OpenAI]] represents the opposite approach — a hosted model API that hides the framework entirely, eliminating the need for self-hosting PyTorch and managing dependencies.
