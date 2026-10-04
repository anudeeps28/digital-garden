---
type: atomic
tags: [mental-model, devops, coding/quality]
date: 2026-10-04
---

# Instrument the Hypothesis

## Idea
When a failure is intermittent, stop arguing about the cause and build a small, temporary probe that will prove or disprove your best guess.

## Definition
Intermittent failures attract theories, and theories attract debate. **Instrumenting the hypothesis** turns the debate into a measurement: write down what you think is happening, then add the narrowest piece of observation that would show it, run it long enough to catch several failures, and let the data decide. The probe is deliberately temporary. Once it has answered the question, it is retired and its log is kept as evidence. A worked example: a scheduled task failed on some nights and not others. A tiny probe that hit the dependency once a minute ran for eight days, roughly 209 probes, and caught five failures, every one at 21:00:01 and every one returning a CDN error. The hypothesis (a nightly edge maintenance window colliding with an on-the-hour schedule) went from plausible to proven, the job was moved off the hour, and the probe was switched off.

## Source
David J. Agans, *Debugging: The 9 Indispensable Rules for Finding Even the Most Elusive Software and Hardware Problems* (2002), especially "Make It Fail", "Quit Thinking and Look", and "Keep an Audit Trail". The broader lineage is the scientific method's demand that a hypothesis predict something observable.

---

## Compass

**Roots** — *where this comes from*
It is the engineering form of [[Consensus Is Not Evidence]]: a team agreeing on a cause is not the same as having seen it. [[Field Verification]] makes the same demand for evidence from the real system rather than from reasoning about it.

**Paths** — *where this leads*
Probes are the cure for [[Silent Failure]], and a probe that proves its worth can graduate into permanent [[Structured Logging]] or a [[Health Probe]]. Its evidence also gives a [[Postmortem]] a timeline instead of a story.

**Neighbors** — *what lives nearby*
[[Prediction Journal]] applies the same discipline to personal forecasts, and the on-the-hour collision is a cousin of the [[Thundering Herd]].

**Clash** — *what pushes against this*
Probes cost time and add load, and some failures are rare enough that waiting for one is too slow. Sometimes [[Fail Fast Fail Loudly]] plus a reasonable guess fixes the problem sooner than a week of measurement.
