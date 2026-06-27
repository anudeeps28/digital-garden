---
type: resource
tags: [coding/distributed-systems, ddia]
date: 2026-03-30
source-type: book
url:
author: Martin Kleppmann
---

# Designing Data-Intensive Applications

## Summary
A deep, practical guide to the internals of distributed data systems — databases, replication, partitioning, transactions, consistency, and batch/stream processing. Covers the *why* behind design decisions, not just the *what*. Essential reading for anyone building or reasoning about systems that store and process data at scale.

## Key Ideas
- Reliability, Scalability, and Maintainability are the three pillars of every data system
- The right data model (relational, document, graph) depends entirely on the shape of your data and access patterns
- Distributed systems introduce partial failures, unreliable networks, and clock skew — these must be designed around, not ignored
- Transactions and isolation levels are a spectrum of tradeoffs between correctness and performance
- Consensus (getting nodes to agree) is the hard unsolved core of distributed systems

## Quotes / Excerpts
> "A fault is usually defined as one component of the system deviating from its spec, whereas a failure is when the system as a whole stops providing the required service to the user."

> "Scalability is not a one-dimensional label... it is meaningless to say 'X is scalable' or 'Y doesn't scale'. Rather, discussing scalability means considering questions like 'If the system grows in a particular way, what are our options for coping with the growth?'"

## My Thoughts
*To be filled as chapters are processed.*

## Atomic Notes Spawned
- [[Fault vs Failure]]
- [[Scalability and Load Parameters]]
- [[Percentile-Based Performance Metrics]]
- [[Maintainability-Operability-Simplicity-Evolvability]]

## Related
- [[Distributed Systems Design]]
- [[Replication]]
- [[Partitioning]]
- [[Transactions and ACID]]
