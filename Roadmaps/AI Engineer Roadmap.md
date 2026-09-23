---
type: roadmap
tags: [ai/llm, roadmap, learning, career]
date: 2026-09-23
---

# AI Engineer Roadmap

Nine steps, 24 weeks. The path I'd actually follow if I started over — weighted by what's genuinely hard and what pays off once you're doing the job, not by what's fun to teach.

> The written version of the video **[Become an AI Engineer in 6 Months (Full 2026 Roadmap)](https://www.youtube.com/watch?v=pw5NM-zml0Y)**.

It took me six months to get my job as an AI engineer. I'd change how I spent about half of it.

---

## The week budget

The weighting is the whole point. Most roadmaps give every step a bullet of equal size. These are not equal.

| # | Step | Weeks |
|---|---|---|
| 1 | Python | 0 (3 if starting cold) |
| 2 | LLM mental model | 1 |
| 3 | LLM APIs in production | 2 |
| 4 | Context engineering | 4 |
| 5 | **RAG & retrieval** | **5** |
| 6 | Agents, tool calling & MCP | 3 |
| 7 | Evals | 3 |
| 8 | Deploy & operate | 4 |
| 9 | Portfolio | 2 (parallel from week 8) |
| | **Total** | **24 weeks** |

Step 7 is the one that isn't on any roadmap I've seen. It's the thing that separates people who can build a demo from people who get paid to ship.

---

## 1 — Python · 0–3 weeks

Python appeared in 82% of 889 real AI engineer job listings. It's not a skill that makes you stand out — it's the floor you stand on.

Most Python courses get this backwards for our purposes. You don't need to grind data structures and algorithms. You need:

- functions and classes
- **HTTP requests**
- **async**

Because almost everything you're about to build is your code talking to somebody else's model over a network, and waiting.

And don't say "I'll make Claude do the work." If you want to go into the weeds, you have to understand at least what your agent is producing.

---

## 2 — LLM mental models · 1 week

You need a working model of what a language model actually is: [[Tokens|tokens]], the context window and why performance degrades well before you hit the limit, temperature, and the role system (system vs user vs assistant).

That's the working set. That's what you need.

**I went a lot deeper than that** — the matrices, the equations, the maths underneath. I did it because I have a master's in robotics and AI and the maths was accessible to me. It was not necessary.

I'm telling you because this is the step where people quit. You start reading about attention mechanisms, you hit linear algebra you haven't touched since university, and you conclude you're not smart enough for this. That's the wrong conclusion.

**The job you're training for is a software engineering job.** AI engineering runs on software engineering. It's the ML engineers who need the statistics and model-architecture depth — different job, different roadmap ([[Machine Learning Roadmap|that one's here]]).

Know what an embedding is. Know why context has a limit. Then move. If you like maths, go deep later — because you enjoy it, not because you think there's a gate.

---

## 3 — LLM APIs · 2 weeks

The frame for this step is **reliability**.

Anyone can make one API call to OpenAI or Anthropic. You'll do it in an afternoon and it'll feel like nothing. That's not what this step is.

This step is what happens when that call fails. Because it will. Rate limit. Timeout. A response that's technically valid and completely useless. A bill you weren't expecting.

Read the actual job listings and this is the language you find: rate limits, retries, cost control, streaming, fallback strategies. Companies aren't asking whether you can call a model. They're asking whether the thing you built stays up.

Build something small that makes real calls, then deliberately break it. Fire too many requests. Handle the failure properly ([[Fail Fast Fail Loudly]]). Add streaming so the user sees tokens arriving instead of a spinner. Watch what it costs, then watch what it costs when you're careless.

You come out understanding that **a model is an unreliable network dependency you don't control.** That's the single most useful thing to believe going into everything that follows.

---

## 4 — Context engineering · 4 weeks

The frame: **what the model sees.**

Every roadmap calls this prompt engineering. That name is out of date, and the change matters because it changes what you practise.

In 2023 the skill was phrasing — you wrote "think step by step" and output got better. Models got good at understanding you, so phrasing stopped being the bottleneck and *what's in front of the model* became the bottleneck.

The number that made it click: in a system running multi-step work with tool calls, your instruction is roughly **5% of what the model sees.** The other 95% is retrieved documents, conversation history, tool definitions, memory, state. [[Prompt Engineering]] optimises the 5%. Context engineering optimises all of it.

Two things live inside this step that you might expect separately:

- **Structured outputs** — JSON back instead of prose you have to parse
- **Function / tool calling** — how the model tells your code to go do something

They used to be their own chapters. Now they're what context engineering looks like in practice: you define the shape of what goes in and the shape of what comes out ([[Define Contract Before Implementation]]), and the model works inside that shape.

Four weeks because there's real practice here. Learn to budget a window. Learn that a bigger context window is **not** permission to dump everything in — accuracy degrades long before the limit ([[Selective LLM Usage]]). Learn what to cut.

---

## 5 — RAG · 5 weeks

More than any other step. If you take one thing from this roadmap, take this.

[[RAG (Retrieval-Augmented Generation)|Retrieval-augmented generation]] appeared in almost **36%** of those 889 listings. More than prompt engineering. More than agents. **Four times more than fine-tuning**, which gets a wildly disproportionate amount of attention online.

**What nobody warns you about:** I built a RAG retrieval system assuming the hard part would be the model — the reasoning, the clever bit. It wasn't. **The hard part was the search.**

The first thing that broke was [[Chunking|chunking]]. It sounds trivial — you split text into pieces, how hard can it be. But chunk too small and you lose the context that made the passage meaningful. Chunk too large and the relevant sentence gets buried next to three paragraphs of noise and retrieval scores it badly. Split in the wrong place and you cut an idea in half. I got that wrong repeatedly before I got it right.

Past chunking, retrieval itself is a grind. Embeddings that look similar mathematically aren't always similar in meaning. You'll add [[Hybrid Search|hybrid search]]. You'll add metadata filtering. You'll add [[Semantic Re-ranking|re-ranking]]. Every one of those exists because pure [[Vector Search|vector similarity]] isn't good enough on its own.

Five weeks not because the concept is complicated — you can explain RAG in one sentence — but because **making it work well is where the actual engineering lives.**

**Skip:** don't get attached to a vector database. Pinecone shows up in under 6% of listings, Weaviate under 5%. Nobody's hiring you for a vendor. Pick anything, learn the pattern, move on.

---

## 6 — Agents, tool calling & MCP · 3 weeks

The frame: **what the model can do**, not just what it sees.

An agent is a model in a loop with tools. It calls something, gets a result, decides what's next. Everything else is plumbing around that loop.

**This is where I'll save you the most time.** Every roadmap tells you to learn an orchestration framework. I built a couple of small projects with LangChain, then stopped and went straight to the raw SDKs — not because the framework was bad, but because I could feel I was learning *the framework* instead of the thing underneath it.

That turned out to be right, and there's data behind it now. Production teams have migrated to the OpenAI Agents SDK, the Claude Agent SDK, or direct API calls, because the model providers absorbed the abstractions the frameworks existed to provide. LangChain appears in under 19% of listings. LangGraph 8%. LlamaIndex under 6%.

Hiring guidance now explicitly tells managers **not** to require a specific agent framework, and to hire instead for the underlying skills: tool calling, structured outputs, eval design, debugging systems that don't give you the same answer twice.

So learn the loop. Learn tool calling properly at the API level. Then pick a framework if you want one, and hold it loosely.

Add **MCP** (Model Context Protocol) here — the standard way to expose tools and data to any model, so you build the connection once instead of rebuilding it per client. It's in real job listings now, sometimes as its own role. Worth a few days.

---

## 7 — Evals · 3 weeks

**This is the gap in the map.**

In regular software you write a test, it passes or fails, same answer every time. Deterministic. Language models are not. Same input, different output.

So what does "working" even mean? You change a prompt to fix one thing — how do you know you didn't break four others? You swap in a cheaper model — is your product better or quietly worse? You cannot answer that by trying it a few times and feeling good about the results. Which is exactly what most people do, including me, for longer than I'd like to admit.

Evals are the answer. A set of test cases with known-good outcomes, run against your system, producing a number. Change something, see whether the number moved. That's the whole idea. It's not exotic — it's the discipline nobody teaches because it isn't fun and it doesn't demo well.

The listing data backs it: evaluation pipelines, observability, guardrails, making system behaviour measurable. A 2026 hiring template states outright that the job description should say the hire will own the eval harness. There are people whose entire title is **evals engineer**. Most roadmaps give this thirty seconds, or nothing.

**What to do:** learn one eval framework. Build a small eval set for whatever you made in step 5 — 20 or 30 cases where you know what good looks like. Then change your chunking strategy and watch the number move. That moment, when you can see whether a change helped, is when you stop guessing and start engineering.

When someone interviews you and you can talk about how you *measured* your system, you will not sound like the other forty candidates who built the same chatbot.

---

## 8 — Deployment · 4 weeks

Second-biggest block, and the one most likely to get skipped, because it's the least glamorous thing here.

Look at what listings actually ask for: **AWS 40%. Docker 31%. CI/CD 29%. Kubernetes 29%.** Every single one bigger than LangChain. The framework everybody argues about online appears in fewer listings than Docker does.

Companies are not hiring people who can make AI work on a laptop.

**And there's an AI-specific part traditional deployment doesn't prepare you for: cost.** Normal software costs roughly the same per user at a thousand users as at one. AI doesn't work like that — every request costs money, and features that look profitable at a thousand users break at a hundred thousand.

So this step includes the things that keep the economics alive:

- **caching** — don't pay twice for the same answer
- **routing** — easy work to a cheaper model, escalate only when needed
- **batching** — anything that isn't real-time
- **cost per task** — track that, not just the total

One 2026 hiring guide called cost optimisation the most underrated skill in AI engineering right now. Most people can build a working RAG system. Far fewer can build one that's still affordable at scale.

Take one thing you built and get it actually running — containerised, deployed, monitored, with a number attached to what it costs per request. That's a different level of credibility than a repo.

---

## 9 — Show it off · 2 weeks (parallel from week 8)

"Build a portfolio" is the emptiest advice in this genre. The question isn't how many projects. **It's what each project proves.**

Mine, as an example:

1. **The RAG system** — proves I can build the standard thing correctly. It's what companies are hiring for, and I can talk about what broke, how I fixed the chunking, why retrieval was harder than the model. It survives follow-up questions.
2. **An open-source harness for Claude Code** — a way to build software with agents in a structured, more deterministic way. Nobody asked for it. There was no tutorial. I built it because I kept hitting the same problem in my own work.

Those prove completely different things. The first proves I can do the job. The second proves I'll build something that doesn't exist yet when the situation calls for it. **One makes you hireable, the other makes you interesting, and most people only ever build the first kind.**

Point them where the demand is — the most common use case in the job data is automating multi-step workflows, then internal operational efficiency, then search over a company's own documents.

---

## Harnesses — not a step, a layer

This doesn't fit as a step because it runs through all nine.

When Claude Code came out I jumped on it immediately — not because it was on a plan, but because it was obviously the thing. That's most of my actual job now: I direct agents, review what they produce, and evaluate whether it's right. I'm not typing most of the code.

A survey of engineer resumes early this year found **fewer than 12%** explicitly mentioned agentic AI tool usage — even among engineers using these tools daily. Pay attention to the judgment you build while using them, because that judgment is the actual skill.

---

## The part that actually matters

These nine steps give you the vocabulary and a real mental model of what's happening under the hood. You need that — you can't work on something you think is magic.

But the technical details are not what makes you good at this job. What makes you good is being able to look at a problem you've never seen, break it down, and work out a solution. Being the person who figures things out.

I learned this stack in six months, and the stack will keep moving. The frameworks I named will change. Some of this will be out of date next year. Your degree and your current specific skills matter less in a world moving this fast than your ability to learn the next thing.

Everything is figureoutable. That's not a motivational line — it's the job description.
