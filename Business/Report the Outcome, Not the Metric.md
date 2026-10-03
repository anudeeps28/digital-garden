---
type: atomic
tags: [business/career, communication, ai/ml]
date: 2026-10-03
---

# Report the Outcome, Not the Metric

## Idea
When you present work, say what changed in the world, not what score your model got.

## Definition
"91% F1" is an answer to a question nobody in the room asked. "Cut manual review time by 40%" is the same result, stated in the units the decision is actually made in. This is not dumbing down — the translation is the harder intellectual move, because it forces you to know who the work is for and what it displaced. It also exposes work that has no outcome: a model with a beautiful score and no behaviour change behind it has nowhere to go when you try to write the sentence. Doing the translation while you build, rather than at the presentation, tends to change what you build.

## Source
From the "how to learn machine learning" video (September 2026): "nobody hiring you cares about the metric, they care about what it did." The surrounding path is the [[Machine Learning Roadmap]].

It is standard counsel in applied data science, and the reasoning is consistent across the practitioner literature: model-quality metrics like F1 and AUC do not tell a stakeholder what the work was worth, so results have to be restated as revenue, cost, time or risk. The usual prescription is to replace the abstract measure with a concrete comparison — not "churn rose 3%" but "we lost 1,510 customers last month."

---

## Compass

**Roots** — *where this comes from*
This is [[Clarity In, Clarity Out]] pointed at your own output — the burden of translation belongs to the person who understands the work, not the person receiving it. It is the reporting-shaped case of [[Explain in Layers]], where you pitch at the listener's level instead of guessing once and hoping.

**Paths** — *where this leads*
Framing work by its effect is most of what separates people who get credit from people who did the work, which is the ground [[How to Make More Money in Your Job]] covers, and it makes the work legible to strangers in the way [[Show Your Work]] argues for.

**Neighbors** — *what lives nearby*
It lives next to [[Managing Ambiguity]], since knowing which outcome counts requires resolving an underspecified question nobody has answered for you. It is the communication end of [[Learn the Loop, Not the Algorithm]] — the evaluation step, stated in the language of the people who asked for the work.

**Clash** — *what pushes against this*
The danger is that outcome claims are far easier to inflate than metrics: an F1 score is falsifiable, while "cut review time by 40%" quietly absorbs every other change that happened that quarter, and nobody can check it — the same unearned fluency [[A Stale Source Is Confidently Wrong]] describes. There are also rooms where the metric *is* the outcome, and translating it for an audience that didn't need the translation reads as evasion, which is the misjudgment [[Selective Intelligence]] warns against.
