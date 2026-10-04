---
type: atomic
tags: [mental-model, framework, learning, ai/llm]
date: 2026-10-04
---

# Tag Claims as Cited or Assumed

## Idea
Label every claim in a piece of research as either `[CITED]` (backed by a source you can point to) or `[ASSUMED]` (believed but not checked), and end with a list of the assumed ones to verify.

## Definition
Research, whether written by a person or an LLM, blends evidence and supposition into one confident voice. Tagging each claim forces the two apart. `[CITED]` means a specific source is attached; `[ASSUMED]` means the claim is plausible, widely repeated, or inferred, but nobody has traced it. The closing **checklist of assumed claims** turns the document from an answer into a set of open questions with an obvious next step. The payoff shows up on popular statistics. A frequently quoted line says that "75% of resumes are auto-rejected by applicant tracking systems before a human sees them". Traced to its origin, the number comes from a 2012 sales pitch by Preptel, a resume-optimisation vendor that went out of business soon after and never published a method or sample. It spread through articles citing articles. Tagged honestly, it would have been `[ASSUMED]` from the start.

## Source
The discipline is formalised in the US intelligence community's **ICD 203 Analytic Standards** (Office of the Director of National Intelligence, 2007, revised 2015), which require products to "properly distinguish between underlying intelligence information and analysts' assumptions and judgments". The ATS myth's origin is documented by several recruiting-industry debunks tracing it to Preptel's 2012 marketing.

---

## Compass

**Roots** — *where this comes from*
It is applied [[Critical Thinking Skills]], and the tag exists because [[Consensus Is Not Evidence]]: a claim repeated a thousand times is still `[ASSUMED]` until someone finds where it began.

**Paths** — *where this leads*
The assumed list feeds naturally into an [[Assumption Register]], and tagging is a cheap guard against model [[Sycophancy]], where an LLM states what you seem to want with borrowed confidence.

**Neighbors** — *what lives nearby*
[[A Stale Source Is Confidently Wrong]] covers the other failure, where a claim is cited but the citation has expired. [[Show Your Work]] is the same instinct for reasoning rather than facts.

**Clash** — *what pushes against this*
Tagging everything slows writing and can make a solid argument read as tentative. Some claims are common knowledge, and demanding a citation for each one is its own kind of noise.
