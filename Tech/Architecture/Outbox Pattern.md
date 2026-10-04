---
type: atomic
tags: [coding/architecture, coding/distributed-systems, coding/patterns]
date: 2026-10-04
---

# Outbox Pattern

## Idea
Don't send a message directly; write it to a durable outbox first, and let a separate relay deliver it whenever the other side is reachable. Nothing is lost if the receiver, or the network, is gone for a while.

## Definition
The classic form is the **transactional outbox**. A service needs to update its database and publish an event to a [[Message Broker]], but it can't do both atomically, so a crash between the two leaves them disagreeing (the **dual-write problem**). Instead it inserts the event into an `outbox` table in the same transaction as the business change. A **message relay** reads the table and publishes, marking rows sent. Either both the change and the intent exist, or neither does. The same shape works far outside microservices as **store-and-forward**. An always-on server that produces notes for a laptop writes them into an outbox folder; when the laptop wakes it pulls with `rsync --remove-source-files`, which deletes each file on the server only after it has been copied. If the laptop is off for a week, the notes just wait. An offline-first web app does the same in the browser: writes go into an IndexedDB queue and are flushed when the connection returns, with a simple rule such as last-write-wins to settle conflicts. Because the relay can crash after sending but before marking, delivery is at least once and receivers must tolerate duplicates.

## Tools
- **Debezium** — change-data-capture that tails the database log and publishes outbox rows.
- **rsync** — `--remove-source-files` turns a folder into a pull-based outbox.
- **IndexedDB / Background Sync** — browser storage and API for queued offline writes.

## Source
Codified as "Transactional Outbox" by Chris Richardson on microservices.io and in *Microservices Patterns* (Manning, 2018). Store-and-forward itself is far older, from telegraph relays and email (SMTP) delivery queues.

---

## Compass

**Roots** — *where this comes from*
It exists because [[ACID Properties]] stop at the edge of one database, and a broker or a sleeping laptop is outside that edge. The relay is what makes [[Idempotency]] on the receiving side mandatory.

**Paths** — *where this leads*
Offline-first clients such as a [[Progressive Web App]] use a [[Service Worker]] to drain the local outbox, and on macOS a [[launchd]] job that fires on wake is a natural relay trigger.

**Neighbors** — *what lives nearby*
The [[Write Ledger]] records which deliveries succeeded, while the outbox records what still needs delivering. [[Publish-Subscribe Pattern]] is what usually sits on the far side of the relay.

**Clash** — *what pushes against this*
Queued writes from offline clients can conflict, and last-write-wins quietly discards the loser. Where that matters you need [[Server-Authoritative State]] or real merge logic, not just a queue.
