---
type: atomic
tags: [coding/database]
date: 2026-05-06
---

# ACID Properties

## Idea
ACID is the set of four guarantees that make [[Relational Database|relational databases]] trustworthy — every transaction either fully succeeds or fully rolls back, and concurrent users never corrupt each other's data.

## Definition
ACID stands for:

**Atomicity** — A transaction is all-or-nothing. If you're transferring money between two accounts (debit one, credit the other), either both happen or neither does. No partial state.

**Consistency** — The database moves from one valid state to another. All rules, constraints, and [[Foreign Key|foreign key]] relationships are enforced. You can't end up with an order pointing to a customer that doesn't exist.

**Isolation** — Concurrent transactions don't interfere with each other. If two users update the same row simultaneously, the database handles it so neither sees a half-finished write.

**Durability** — Once a transaction is committed, it survives crashes, power failures, etc. The data is permanently saved.

These guarantees are what make relational databases suitable for financial systems, healthcare records, and any domain where data integrity is critical. [[PostgreSQL]] has particularly strong ACID compliance using MVCC (Multi-Version Concurrency Control) for isolation.

## Source
Conversation with Claude — relational databases and PostgreSQL

---

## Compass

**Neighbors** — *what lives nearby*
Schema changes are themselves transactions that should be atomic, just like [[Database Migrations]]. ACID is itself a defining characteristic of [[Relational Database|relational databases]].

**Clash** — *what pushes against this*
[[NoSQL|NoSQL databases]] trade ACID guarantees for performance and scalability, embracing [[eventual consistency]] instead. The BASE model (Basically Available, Soft state, Eventual consistency) represents the opposing philosophy to ACID.

**Roots** — *where this comes from*
ACID is the foundational reason why [[Relational Database|relational databases]] are trusted for critical data. The core question underlying ACID is: what tradeoffs do you accept when choosing eventual consistency over ACID guarantees?

**Paths** — *where this leads*
[[PostgreSQL]] is particularly known for strong ACID compliance via MVCC (Multi-Version Concurrency Control), and understanding ACID shapes how you approach transaction management in application code.
