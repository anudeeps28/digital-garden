---
type: atomic
tags: [mental-model, framework, business/strategy, ai/agents]
date: 2026-10-04
---

# One-Way and Two-Way Doors

## Idea
Sort decisions by whether you can walk back through them, then spend deliberation only on the ones you can't.

## Definition
A **one-way door** is a decision that is expensive or impossible to undo: deleting data, signing a contract, publishing a public API. A **two-way door** is reversible: a default setting, a variable name, which of two libraries to try first. The skill is classification, not caution. Treating every choice as a one-way door produces slowness and timid experiments; treating every choice as a two-way door eventually walks you off a cliff. The framing turns out to be an excellent delegation rule for AI agents. An agent can self-answer reversible choices with its recommended option and log each one under "decisions made on your behalf" in the pull request, so a human can reverse any of them in seconds. It should pause and ask when a choice is irreversible, contradicts an earlier instruction, changes scope, depends on something missing, or has failed three attempts. And it should never quietly substitute a stand-in for a named tool or agent that isn't available, because that swap looks reversible but silently changes what was asked for.

## Source
Jeff Bezos, Amazon 2015 letter to shareholders, which calls irreversible decisions "Type 1" (one-way doors, to be made "methodically, carefully, slowly") and reversible ones "Type 2" (to be made quickly by small groups), and warns that large organisations drift into using the heavy Type 1 process for everything.

---

## Compass

**Roots** — *where this comes from*
It is [[Read-Only by Default]] applied to judgement: be strict exactly where mistakes stick, and loose everywhere else. It also borrows from [[The Dichotomy of Control]], separating what can still be changed from what can't.

**Paths** — *where this leads*
The logged list of self-answered choices is a form of [[Show Your Work]], and the pause conditions become the rules behind a [[Needs-You Inbox]] or a [[Propose, Don't Execute]] agent.

**Neighbors** — *what lives nearby*
[[Grill the Plan]] spends its energy on the one-way doors in a design, and [[Rollback Scripts]] are a way of turning a one-way door into a two-way one.

**Clash** — *what pushes against this*
Many doors look two-way and aren't: a "temporary" default that users build habits around, or a schema that other systems start reading. [[Blast Radius]] is often the better test of reversibility than the decision's surface.
