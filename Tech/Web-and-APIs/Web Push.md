---
type: atomic
tags: [web, frontend, api]
date: 2026-10-04
---

# Web Push

## Idea
Web Push lets a server send a notification to a user's browser or installed web app even when the page is closed.

## Definition
The browser subscribes through the **Push API**, which returns a subscription: an endpoint URL on the browser vendor's push service plus encryption keys. Your server stores that subscription and, when something happens, sends an encrypted message to the endpoint. The push service wakes the site's [[Service Worker]], which shows the notification. Servers identify themselves with **VAPID**, a signed token proving which application server is sending, so no vendor account is needed. Two operational lessons dominate. First, subscriptions die: the push service answers `404` or `410 Gone` for expired ones, and you must delete them rather than retry forever. Second, on iOS, web push only works for a [[Progressive Web App]] added to the home screen, and subscriptions can expire silently with no error. The robust pattern is to re-subscribe on every app launch and send the fresh subscription to the server, prune on `410`, and keep an **in-app fallback** (a badge or nudge shown on next open) so nothing important depends on push arriving.

## Providers
- **Browser push services** — Google FCM for Chrome, Mozilla autopush for Firefox, Apple's push service for Safari; all speak the same protocol.
- **Libraries** — `web-push` (Node) and `pywebpush` (Python) handle encryption and VAPID signing.

## Source
IETF RFC 8030, Generic Event Delivery Using HTTP Push (December 2016); RFC 8291 for message encryption; RFC 8292, VAPID (November 2017); W3C Push API. Safari added web push for home-screen web apps in iOS 16.4 (2023).

---

## Compass

**Roots** — *where this comes from*
It depends entirely on the [[Service Worker]], the only part of a site that can run while no tab is open, and it was one of the features that made the [[Progressive Web App]] idea credible against native apps.

**Paths** — *where this leads*
Treating delivery as best-effort pushes you toward [[Graceful Degradation]], and pruning dead subscriptions on [[HTTP Status Codes|410 Gone]] keeps the send loop cheap.

**Neighbors** — *what lives nearby*
A [[WebSocket]] delivers instant updates while the app is open; push covers the time it is closed. [[Exponential Backoff]] applies to the transient 429 and 5xx answers from push services.

**Clash** — *what pushes against this*
Platform rules decide whether it works at all, and silent expiry means a push-only design is a [[Silent Failure]] waiting to happen.
