---
type: atomic
tags: [coding/distributed-systems, coding/architecture, coding/azure, devops]
date: 2026-10-01
---

# Message Broker

## Idea
A message broker is a holding area between the part of a system that creates work and the part that does it, so neither has to be running, or keeping up, at the same moment as the other.

## Definition
A message broker is middleware that accepts messages from **producers**, stores them durably, and hands them to **consumers** when they are ready. Because the broker holds the message, the producer can finish and move on even if the consumer is down, slow or scaled to zero, and a burst of work just becomes a longer line. It offers two shapes. A **queue** gives each message to exactly one consumer, which spreads work across workers. A **topic** (publish/subscribe) gives every subscriber its own copy, so one event can fan out to several independent handlers. Most brokers promise **at-least-once delivery**: if a consumer takes a message and crashes before confirming it, the message comes back and is delivered again. Consumers therefore have to be **idempotent**, meaning that processing the same message twice gives the same result as processing it once. A message that keeps failing is moved to a **dead-letter queue** after a set number of attempts, so one bad message doesn't block everything behind it, and someone has to watch that queue. **Ordering** isn't guaranteed by default; strict order usually means grouping related messages (sessions, partition keys) and accepting less parallelism.

## Providers
- **Azure** — Azure Service Bus (queues and topics, sessions, dead-lettering); Storage Queues for simple, cheap queues; Event Grid for push-style event routing.
- **AWS** — Amazon SQS (queues) and SNS (pub/sub fan-out), often combined; EventBridge for event routing.
- **Google Cloud** — Pub/Sub (topics and subscriptions, optional ordering keys).
- **Others** — RabbitMQ (open-source, AMQP); Apache Kafka, which is really a replicated append-only log rather than a classic broker: messages aren't removed when read, and each consumer tracks its own position, so it can replay history.

## Source
Message-oriented middleware goes back to IBM MQSeries (1993); the queue and publish/subscribe patterns are catalogued in *Enterprise Integration Patterns* (Hohpe and Woolf, 2003). AMQP 1.0 became an OASIS standard in 2012.

---

## Compass

**Roots** — *where this comes from*
It comes from decoupling in distributed systems: when services call each other directly, one slow service slows down every caller.

**Paths** — *where this leads*
Queues are the standard trigger for [[Serverless Functions]] and [[Scale-to-Zero|scaled-to-zero]] workers; failed messages are retried with [[Exponential Backoff]] before being dead-lettered.

**Neighbors** — *what lives nearby*
[[Graceful Degradation]]: accepting a request into a queue and processing it later is often the most graceful way to survive a downstream outage. [[Rate Limiting]] handles the same kind of overload from the other side.

**Clash** — *what pushes against this*
It adds a moving part and makes failures harder to see. Work is now "accepted but not done", so you need idempotency, dead-letter monitoring and end-to-end tracing. For a simple request that needs an answer right away, a direct call is clearer.
