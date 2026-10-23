---
type: atomic
tags: [mental-model, systems-thinking]
date: 2026-10-23
---

# Stocks and Flows

## Idea
A stock is an amount that has built up over time. Flows are the rates that fill or drain it. You can only change a stock by changing its flows, and that takes time.

## Definition
Picture a bathtub. The water in it is the stock: something you could count or measure at a single moment. The tap is the inflow and the drain is the outflow. Bank balances, inventory, trust, skills, reputation, carbon in the atmosphere and technical debt are all stocks. Three things follow. First, if inflow exceeds outflow the stock rises, whatever the absolute numbers are, so you can grow it by slowing the drain as well as by opening the tap. Second, stocks change slowly, because even a big flow needs time to fill or empty them. Third, that slowness acts as a buffer, which lets inflows and outflows get out of step without the system breaking. Stocks also make a system easy to diagnose, because they are visible and measurable even when the connections between parts are not.

## Source
Donella H. Meadows, *Thinking in Systems*, Chapters 1–2. Stock-and-flow diagrams come from Jay Forrester's system dynamics. See [[Thinking in Systems]].

---

## Compass

**Roots** — *where this comes from*
Stocks and flows are the basic objects of [[Systems Thinking]], what the system is made of, while feedback loops describe how it steers itself.

**Paths** — *where this leads*
Once a stock's level controls its own flows, you have a [[Balancing Feedback Loop]] or a [[Reinforcing Feedback Loop]]. Whether a resource runs out because of its stock or its flow is the point of [[Stock-Limited vs Flow-Limited Resources]].

**Neighbors** — *what lives nearby*
[[Backpressure]] is stock-and-flow thinking in software: a queue is a stock, and if arrivals keep exceeding service, it grows until something breaks. [[Kanban]] makes the stocks of work in progress visible so the flows can be managed. [[Consistency Over Intensity]] is the human version: a skill is a stock filled by small daily inflows.

**Clash** — *what pushes against this*
The buffering that keeps systems stable also hides problems. A large stock can absorb a bad outflow for years before anyone notices, which is how [[Drift to Low Performance]] and depleting commons stay invisible until late.
