---
type: roadmap
tags: [ai/ml, roadmap, learning, career]
date: 2026-09-23
---

# Machine Learning Roadmap

The six-month path I'd take if I were learning machine learning from scratch today.
Six to eight months to get genuinely good, at ten hours a week. That's the real number.

> The written version of the video **How I Would Learn Machine Learning in 2026 (If I Started Over)**.

---

## Before you start

**This is the ML path, not the AI-engineering one.** They're different jobs. If what you want is to build applications on top of models — RAG, agents, LLM APIs — the [[AI Engineer Roadmap]] is the one you want. ML engineering is where the statistics and model-architecture depth actually live.

**Python has to be solid.** That's the honest prerequisite. If it isn't, do that first — everything after this gets easier.

**You do not need the math first.** Most roadmaps open with linear algebra, calculus and probability, and tell you that you're allowed to touch a model afterwards. I did it that way, enjoyed it, and it's the single thing that cost me the most time. Fun is not the same as getting good.

The math that actually matters:

| | When |
|---|---|
| **Statistics** | The main one. Worth real time. |
| Linear algebra | Later, on demand, when something blocks you. |
| Calculus | Same. You don't need to be good at it to start. |

When you get stuck — and you will, once — go to 3Blue1Brown or StatQuest, learn exactly the piece that's blocking you, and come back. That's the whole math strategy. It's the same reason [[We Learn by Doing, Not by Watching]] holds here: the theory sticks when it arrives attached to a problem you already have.

---

## Months 1–2 — Python and the loop

Get comfortable with numpy, pandas, and one scikit-learn project end to end.

Something like an email classifier — is this spam, is this important, what folder does it go in. Or a weather predictor. It genuinely doesn't matter which.

What you're actually learning here is **not the algorithm**. It's the loop:

```
get data → clean it → train something → measure whether it worked → do it again
```

That loop is the entire job. The algorithms change every year. The loop doesn't. Worth knowing the difference between [[Supervised Learning]] and [[Unsupervised Learning]] at this stage, and not much more theory than that.

**Skip:** don't disappear into Kaggle. A Grandmaster rank is still a real signal. A top-ten-percent finish on clean competition data is, in 2026, closer to a red flag than a resume boost — it proves you can optimise a metric, not that you can ship.

---

## Months 3–4 — Deep learning, by building

**PyTorch.** Not TensorFlow — PyTorch has overtaken it in job postings (39.8% vs 37.5%). Not JAX either; JAX is a research and TPU tool. Even Karpathy ships PyTorch.

**Course:** [fast.ai](https://www.fast.ai/) or Karpathy's [Neural Networks: Zero to Hero](https://karpathy.ai/zero-to-hero.html). Both free. Both put a model in your hands in lesson one.

**Project — this is the magic moment.** Real-time object tracking with YOLO on your webcam. Count people walking past. Track a ball. Whatever's in front of you.

Two reasons: hiring managers specifically call out real-time computer vision right now, and the first time bounding boxes draw themselves around your own face, you understand why people do this for a living. Mine was a YOLO capstone, and it's the thing that flipped the switch — not any of the theory that came before it.

You learn deep learning by building, not by deriving backprop on paper.

---

## Months 5–6 — LLMs, and ship one thing

This is the part most roadmaps put last or leave out. It's the part that got me hired.

**How LLMs actually work** — Karpathy's LLM playlist, start to finish.

**Then vectors and indexing.** This was the first thing that mattered on day one of real work — not a model. How a sentence becomes a list of numbers ([[Vector Embedding]]), how you search a million of those in milliseconds ([[Vector Search]]), how the model gets the right context handed to it ([[RAG (Retrieval-Augmented Generation)]]). None of my courses started there. All of them should have.

**The contrarian bit:** most roadmaps say six months of classic ML first, then maybe LLMs. I'd flip it. Two or three classic projects to learn the loop, then straight here — because this is where the jobs are. LLM and RAG skills carry a $20K–$50K premium in 2026. And these fields are new enough that the courses are being written while you learn them. You're not behind. Nobody's ahead.

**Capstone:** a RAG assistant over one niche corpus. A textbook. A company's docs. Your own notes.

Build the retrieval yourself — embeddings, a vector index, the retrieval step, the answer — and **deploy it with a public URL**. Railway, Cloud Run, a cheap VPS. Somebody who isn't you has to be able to open it and ask it a question.

*Stretch, if you finish early:* fine-tune a small open model on one narrow task and serve it. Strongest signal you can put on a portfolio right now.

**Skip:** LangChain. Famous, and I've never needed it. Build the pipeline yourself once and you'll understand what every framework is hiding from you.

---

## The three projects

Three projects. Three kinds of data. One thing deployed.

1. **Email classifier** — tabular
2. **Webcam YOLO tracking** — vision
3. **Deployed RAG assistant** — text

Three to five end-to-end projects beat fifteen tutorials. A project nobody can open is a notebook, not a portfolio.

---

## What the job actually is

It isn't research and it isn't deriving things. It's using libraries and ML principles to get an output the business needs. AI engineering roles even more so — hands-on, application-based.

The tools I actually touch every week: **PyTorch, OpenCV, Hugging Face.** That's the list.

57.7% of hiring managers now prefer someone who can keep a model alive in production over a generalist who knows every algorithm.

And when you show the project, don't say *"91% F1."* Say *"cut manual review time by 40%."* Nobody hiring you cares about the metric. They care about what it did.

---

## Resources

- **Andrew Ng — ML Specialization** — theory and intuition reference
- **[fast.ai — Practical Deep Learning](https://www.fast.ai/)** — free, code-first, a model in lesson one
- **[Karpathy — Neural Networks: Zero to Hero](https://karpathy.ai/zero-to-hero.html)** — free, backprop and GPT from scratch
- **Karpathy — nanochat** — "train your own ChatGPT for $100," capstone reference
- **3Blue1Brown** and **StatQuest** — math intuition, on demand only

---

## One last thing about the timeline

Free online courses have a 5–15% completion rate. Not because people are lazy — because they were promised three weeks and hit month two. Give yourself the real six to eight months and you're already ahead of most of the people who started with you. This is a [[Consistency Over Intensity]] problem far more than a talent one.

The math — pick it up when it blocks you. Not before.

I lost months to that. Loved every one of them. Wouldn't do it again.
