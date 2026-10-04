---
type: atomic
tags: [coding/embedded]
date: 2026-10-04
---

# GPIO and Open-Drain Outputs

## Idea
A general-purpose pin can be an input or an output, and an output can either actively drive both levels (push-pull) or only pull low and let a resistor bring it high (open-drain). Open-drain is what lets several devices safely share one wire.

## Definition
A **GPIO** pin is configured through registers for **direction** (input or output), **mode** (push-pull, open-drain, alternate function, analog), optional internal **pull-up or pull-down** resistors, and sometimes speed. A **push-pull** output has a transistor to each rail and actively drives 0 or 1. An **open-drain** (open-collector on bipolar parts) output has only the low-side transistor: it can pull the line to ground or let go, and an external or internal **pull-up** resistor brings the line high when nobody is pulling. Connect several open-drain outputs to one line and any device can force it low while none can fight another into a short circuit. The line reads high only when every device has released it, a **wired-AND**. That is exactly how I2C's SDA and SCL lines work, and how two chips can share a reset or "done" line: each holds it low while busy, and it rises only when the last one finishes. A worked example: a board where two processors handed a shared ready line back and forth used push-pull outputs on both sides, and a brief overlap shorted the drivers; switching both to open-drain with one pull-up made the hand-off safe by construction.

## Source
Open-collector outputs date from 1960s TTL logic families and were used for wired-AND buses. Philips' I2C bus (1982) made open-drain signalling a standard for chip-to-chip links. Pin modes are documented per microcontroller in vendor reference manuals.

---

## Compass

**Roots** — *where this comes from*
Every pin setting is a few bits written through [[Memory-Mapped IO]], and the wired-AND trick is plain boolean logic of the kind in [[Bit Manipulation]].

**Paths** — *where this leads*
A GPIO input wired to a button needs [[Switch Debouncing]], and an input edge can trigger an [[Interrupt Service Routine]] instead of being polled.

**Neighbors** — *what lives nearby*
A shared open-drain line is a tiny hardware [[Message Broker]] with one rule: anyone may say "not yet", and "go" means everyone agreed.

**Clash** — *what pushes against this*
The pull-up makes rising edges slow, so open-drain lines trade speed for safety, and push-pull remains the right choice for fast single-owner signals like SPI clocks.
