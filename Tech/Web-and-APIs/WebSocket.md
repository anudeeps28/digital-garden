---
type: atomic
tags: [web, api, coding/web-api, coding/networking]
date: 2026-10-04
---

# WebSocket

## Idea
A WebSocket turns one HTTP request into a long-lived, two-way pipe, so the server can push updates the moment they happen instead of waiting to be asked.

## Definition
A WebSocket connection starts life as an ordinary HTTP request carrying an `Upgrade: websocket` header. If the server agrees, it answers `101 Switching Protocols` and the same TCP connection becomes a **full-duplex** channel: either side can send small framed messages at any time, with no new request per message and no polling. That makes it the natural transport for chat, live dashboards, multiplayer state and collaborative tools. A clean pattern for shared state is: on connect, the server sends the **full current state**; after every accepted change, it broadcasts the new state (or a diff) to everyone in the room. A shared countdown-timer room built this way never drifts, because clients render what the server says rather than running their own clocks. The price is that you now own connection lifecycle: reconnects with [[Exponential Backoff]], heartbeats to detect dead sockets, and re-sending state after a reconnect. Messages arriving over the socket are untrusted input like any request body, so they need parsing and validation, and the handshake needs an origin check because browsers send cookies on it.

## Source
Proposed during HTML5 work by Ian Hickson and others around 2008; standardised by the IETF as RFC 6455 (Ian Fette and Alexey Melnikov, December 2011), with the browser API specified by WHATWG/W3C.

---

## Compass

**Roots** — *where this comes from*
It grew out of the limits of the [[REST API|request-response model]], where the only way to hear about changes was to poll or hold a request open, and it reuses the [[Request and Response|HTTP handshake]] purely to get through existing ports and proxies.

**Paths** — *where this leads*
Once clients receive pushed state, [[Server-Authoritative State]] becomes the obvious design: the server owns the truth and clients just render it. Every incoming frame should pass through [[Runtime Schema Validation]] before it touches that state.

**Neighbors** — *what lives nearby*
[[Web Push]] reaches users when the tab is closed, which a socket cannot, and the [[Publish-Subscribe Pattern]] is the shape most socket servers take internally when broadcasting to rooms.

**Clash** — *what pushes against this*
Because the handshake carries cookies but is not covered by CORS, a careless server is open to [[Cross-Site WebSocket Hijacking]]. Long-lived connections also fight [[Stateless Services]] and scale-to-zero hosting, since each instance now holds sticky in-memory connections.
