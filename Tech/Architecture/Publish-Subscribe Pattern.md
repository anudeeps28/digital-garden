---
type: atomic
tags: [coding/architecture, coding/distributed-systems, coding/patterns, ai/robotics]
date: 2026-10-04
---

# Publish-Subscribe Pattern

## Idea
Publishers send messages to a named topic without knowing who is listening, and subscribers receive everything on the topics they care about without knowing who sent it. Senders and receivers are decoupled in identity, in number and often in time.

## Definition
In **publish-subscribe**, communication goes through **topics** (or channels) rather than direct addresses. A publisher emits a message; the infrastructure delivers a copy to every current subscriber. Adding a new consumer means subscribing, with no change to the producer. That makes it a natural fit for **streams of state** such as sensor readings, prices or status updates, where many parts of a system want the latest value. The contrast is **request/response**, where a caller asks one specific service a question and waits for an answer. Robotics middleware shows both side by side: in ROS, nodes publish typed messages on topics (a laser scanner publishes scans at 10 Hz; mapping, obstacle avoidance and a visualiser all subscribe), while one-off queries like "plan a path from A to B" are **services**, a request/response call. Delivery guarantees vary widely: fire-and-forget, at-least-once with acknowledgements, or retained "last value" for late joiners. Choosing which one you have is part of the design.

## Tools
- **ROS / ROS 2** — topics for streams, services and actions for calls; ROS 2 runs on DDS.
- **MQTT** — lightweight broker-based pub/sub, common in IoT.
- **Cloud and broker services** — Kafka, Google Pub/Sub, Azure Service Bus topics, Redis pub/sub.

## Source
Birman and Joseph's Isis toolkit (1987) offered a "news" service that is generally cited as the first widely used topic-based publish-subscribe system. ROS (Quigley et al., 2009) brought the topic/service split to robotics.

---

## Compass

**Roots** — *where this comes from*
It is usually carried by a [[Message Broker]], and it is the in-process Observer pattern from [[Design Patterns (Gang of Four)]] stretched across a network.

**Paths** — *where this leads*
Reliable publishing from a database-backed service leads to the [[Outbox Pattern]], and consumers that may see a message twice need [[Idempotency]].

**Neighbors** — *what lives nearby*
[[Request and Response]] is the other half of the toolbox, and [[RxJS Observable|observables]] give the same subscribe-to-a-stream model inside a frontend.

**Clash** — *what pushes against this*
Nobody owns the end-to-end flow, so a dropped subscriber becomes a [[Silent Failure]], and fast publishers can overwhelm slow subscribers unless the system applies [[Backpressure]].
