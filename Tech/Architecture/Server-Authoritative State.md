---
type: atomic
tags: [coding/architecture, coding/distributed-systems, web]
date: 2026-10-04
---

# Server-Authoritative State

## Idea
In a shared, real-time app, one server process owns the true state. Clients only send intents ("I want to do X"); the server decides what actually happens and tells everyone.

## Definition
With **server-authoritative state**, clients never write shared state directly. Each client sends an **intent** message, the server **validates** it (is it this player's turn? is the room still open?), applies it to the canonical state, and **broadcasts** the result to every connected client. Clients render whatever the server says. A small multiplayer app built this way might run one process per "room" holding that room's state in memory, connected to clients over WebSockets. Because a single process handles messages one at a time, writes are naturally **serialised**: two people clicking at once just become two messages in order. That removes the need for conflict-free replicated data types (CRDTs) or merge logic, which exist to reconcile writes that happened in parallel on different machines. It also removes a whole class of cheating and desync bugs, since a client can't claim an outcome the server didn't approve. The price is latency: every action makes a round trip, so games add **client-side prediction**, showing the expected result immediately and correcting it if the server disagrees.

## Source
The model comes from multiplayer game netcode. John Carmack's QuakeWorld (1996) paired an authoritative server with client-side prediction to make internet play workable; Valve's Yahn Bernier described lag compensation for the Source engine in 2001, and Gabriel Gambetta's "Fast-Paced Multiplayer" articles are a popular modern explanation.

---

## Compass

**Roots** — *where this comes from*
It is [[Single Source of Truth]] applied to live, shared state, delivered over a persistent [[WebSocket]] connection so the server can push updates.

**Paths** — *where this leads*
The server's core is naturally a [[Reducer Pattern]]: take the current state and an intent, return the next state, broadcast if it changed. Timers and countdowns follow [[Persist Facts, Derive State]] so the server doesn't have to broadcast every tick.

**Neighbors** — *what lives nearby*
Client-side prediction is the same move as [[Optimistic UI]]: show the likely result now, reconcile with the authority later. A [[Shared Contract Package]] keeps the intent and broadcast message shapes identical on both sides.

**Clash** — *what pushes against this*
One process per room is a single point of failure and a scaling ceiling, which is why [[Stateless Services]] are the default elsewhere. Offline or peer-to-peer collaboration, where no server is reachable, is exactly where CRDTs and the [[Outbox Pattern]] come back.
