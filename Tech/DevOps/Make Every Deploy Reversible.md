---
type: atomic
tags: [tech/devops, deployment, framework]
date: 2026-11-04
---

# Make Every Deploy Reversible

## Idea
If going back to the last working version is one fast, practised step, deploys stop being scary and you can ship more often.

## Definition
A deploy is reversible when you can return to the previous known-good version in minutes, without hand edits or heroics. That takes a few habits: keep the previous [[Build Artifacts|build artifact]] instead of rebuilding it, use the [[Runtime Config (Build Once Deploy Everywhere)|same artifact in every environment]], and make [[Database Migrations]] backward-compatible so old code still runs against the new schema. Patterns like blue-green deploys (keep the old version running and switch traffic) and feature flags (switch features off without redeploying) make the switch nearly instant. **Roll back first, debug second**: when a deploy breaks production, the job is to restore service, not to find the bug live.

## Source
Jez Humble and David Farley's *Continuous Delivery* (2010) and Martin Fowler's "BlueGreenDeployment" (2010); the "roll back first" stance is standard in Google's *Site Reliability Engineering* book (2016).

---

## Compass

**Roots** — *where this comes from*
It is the deploy-time version of [[One-Way and Two-Way Doors]]: a release you can undo is a two-way door, so you can go through it fast.

**Paths** — *where this leads*
Easy rollback is what makes frequent shipping through a [[CI-CD Pipeline]] safe, and it shrinks the [[Blast Radius]] of any single bad change, which keeps [[Postmortem|postmortems]] short.

**Neighbors** — *what lives nearby*
[[Rollback Scripts]] do the same job for the database, and a [[Restore Drill]] is the same "practise it before you need it" idea applied to backups.

**Clash** — *what pushes against this*
Not everything can be undone: a destructive migration, an email already sent, or data already corrupted won't roll back with the code, which is why those changes need [[Map Before You Delete|extra care]] before they ship.
