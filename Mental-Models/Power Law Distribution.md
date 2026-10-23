---
type: atomic
tags: [mental-model, statistics, inequality]
date: 2026-10-23
---

# Power Law Distribution

## Idea
In many systems, a tiny number of items account for most of the total, so "average" is misleading and the extreme cases matter most.

## Definition
In a normal (bell-curve) distribution, like height, most values cluster near the mean and extremes are rare and mild. In a power-law distribution, like wealth, book sales, city sizes, startup returns or YouTube views, there is no typical value. A few giants dominate and a long tail of small ones makes up the rest. Power laws tend to appear when outcomes compound, meaning each gain makes the next one easier, so they are the statistical signature of reinforcing loops. The practical consequences: averages mislead, one outlier can outweigh everything else combined, and in such domains strategy is about getting exposure to the rare big win rather than optimizing for the median.

## Source
Vilfredo Pareto's observations of income distribution (1896) are the origin. George Kingsley Zipf (1949) found the pattern in word frequencies and city sizes. Nassim Nicholas Taleb's *The Black Swan* (2007) popularized the "Mediocristan vs Extremistan" framing. Connected here through a video on inequality that discussed the [[Matthew Effect]].

---

## Compass

**Roots** — *where this comes from*
It is the statistical outcome of the [[Matthew Effect]] and [[Success to the Successful]]: when advantage compounds, distributions grow long tails.

**Paths** — *where this leads*
It explains why [[Volume Negates Luck]] works in creative and startup fields: when rare hits dominate, the number of attempts matters more than the quality of an average attempt. [[Metcalfe's Law]] explains why network markets are especially skewed.

**Neighbors** — *what lives nearby*
The [[Pareto Principle]] is the everyday rule of thumb for a power law. [[Percentile-Based-Performance-Metrics]] exist for the same reason: in long-tailed latency, the mean hides the requests that hurt.

**Clash** — *what pushes against this*
Many things labeled power laws are actually log-normal or other heavy-tailed distributions, and fitting a straight line on a log-log plot is famously unreliable (Clauset, Shalizi and Newman, 2009). Saying "it's a power law" can be overconfident.
