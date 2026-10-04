---
type: atomic
tags: [coding/architecture, coding/distributed-systems, coding/patterns]
date: 2026-10-04
---

# Idempotency

## Idea
An operation is idempotent when running it twice leaves the world in the same state as running it once. Since schedulers, retries and humans all re-run things, idempotency is what makes "run it again" a safe answer.

## Definition
Real systems deliver **at least once**: a cron job fires twice after a clock change, a retry resends a request whose reply was lost, someone re-runs a script to be sure. You cannot stop duplicates from arriving, so you make them harmless. The practical recipe for "exactly once" is **at-least-once delivery plus a durable done-marker**: before acting, check whether this item is already done; after acting, record that it is. The marker must outlive the process and the machine, and ideally lives on the source record itself, written by exactly one actor. For example, a job that copies new items to another system sets a "processed" checkbox on each item once it succeeds. When the server was rebuilt from scratch, nothing was copied twice, because the memory of what was done lived in the data, not on the box. That same property let the job move from hourly to every five minutes with no new risk. Provisioning scripts follow the same rule as **check-then-create**: look for the resource, create it only if missing, so the script can be run a hundred times and converge to one result. HTTP bakes this in: `GET`, `PUT` and `DELETE` are defined as idempotent, `POST` is not, which is why payment APIs accept an **idempotency key** on POST.

## Source
The word comes from mathematics (Benjamin Peirce, 1870: an element that equals itself when multiplied by itself). For distributed systems, Pat Helland's "Idempotence Is Not a Medical Condition" (ACM Queue, 2012) is the classic argument that retried messages make idempotence essential. HTTP method idempotency is defined in RFC 7231 (2014), now RFC 9110 (2022).

---

## Compass

**Roots** — *where this comes from*
It grows out of the fact that networks lose replies, so [[Exponential Backoff]] and every other retry policy will eventually resend something that already succeeded. The semantics of [[HTTP Methods]] encode which verbs promise to survive that.

**Paths** — *where this leads*
When one input fans out to several destinations, a single done-flag is too coarse, which leads to a per-destination [[Write Ledger]]. [[Migration Scripts]] that check before they alter are the same idea applied to schemas.

**Neighbors** — *what lives nearby*
The [[Outbox Pattern]] relies on consumers being idempotent because its relay may publish a message twice. A scheduled job under [[Cron]] is the most common place this bites first.

**Clash** — *what pushes against this*
Some actions are inherently not repeatable, like sending an email or charging a card, and there the done-marker must be written atomically with the side effect or you only move the window. [[ACID Properties]] give you that atomicity inside one database, but not across two systems.
