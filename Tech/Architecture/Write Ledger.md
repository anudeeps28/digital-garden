---
type: atomic
tags: [coding/architecture, coding/distributed-systems, coding/patterns]
date: 2026-10-04
---

# Write Ledger

## Idea
When one input has to be written to several destinations, track success per (item, destination) pair, not per item. Otherwise one permanently failing destination makes every successful one repeat forever.

## Definition
A **write ledger** is a small durable record, often just a file or a table, with one row for each item and each destination it must reach, marked done when that specific write succeeds. On each run the job only attempts the pairs that are not yet done. The failure it prevents is subtle. Picture a job that takes each new item and writes it to three places, then marks the item "processed" only when all three succeed. One destination starts returning 404 for good. The item never gets marked, so every hourly run rewrites it to the two healthy destinations. What looked like a "rare duplicate" was actually **unbounded**: around 200 duplicates piled up before anyone noticed. With a ledger, the two successful writes are recorded once and never repeated, and the broken destination fails alone and visibly. Keep the ledger logic in **pure helpers** (given the ledger and the item, which pairs are pending; given a result, what is the new ledger) so the edge cases can be covered by fast unit tests without touching the network.

## Source
"Write ledger" is a descriptive name rather than a coined pattern. The idea follows Pat Helland's "Life beyond Distributed Transactions" (CIDR, 2007), which argues that without distributed transactions each entity must remember which messages it has already processed, and it is the same bookkeeping that idempotency-key tables in payment APIs perform.

---

## Compass

**Roots** — *where this comes from*
It is [[Idempotency]] at finer grain: the done-marker moves from the item to each destination the item must reach. It also answers the question [[ACID Properties]] can't, because there is no single transaction spanning three external systems.

**Paths** — *where this leads*
Per-destination records make [[Silent Failure]] detectable, since you can alert on the one pair that keeps failing instead of the whole run. Writing the logic as [[Pure Functions]] is what makes it cheap to test thoroughly with [[Unit Tests]].

**Neighbors** — *what lives nearby*
The [[Outbox Pattern]] stores intent before sending; the ledger stores outcome after sending, and many systems use both. Containing one bad destination is also a [[Blast Radius]] decision.

**Clash** — *what pushes against this*
A ledger is extra state that can itself drift from reality, for example if someone deletes the copy at a destination by hand. The principle of a [[Single Source of Truth]] argues for checking the destination directly when that is cheap enough.
