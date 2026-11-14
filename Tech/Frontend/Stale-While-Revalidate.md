---
type: atomic
tags: [tech/frontend, tech/performance, tech/caching]
date: 2026-11-14
---

# Stale-While-Revalidate

## Idea
Show the last copy instantly, fetch fresh data in the background, then update the screen: that is most of what makes an app feel fast.

## Definition
An app that asks a slow service for live data every time a screen opens makes the user wait for that service every time. Stale-while-revalidate turns this around. It keeps a copy of the last response on the device, renders it immediately, starts a background request for fresh data, and swaps the new data in when it arrives. The user sees content in milliseconds, and it is at most one refresh out of date. Two habits make it work well. **One request per screen:** fetch everything a screen needs in one call instead of many small ones, so there is just one thing to cache and revalidate. **Assume the slow part is a third party:** the delay is usually an outside service (a hosted database or a SaaS API), not your own code, so that is the call to cache. Taken further, this becomes *offline-first*: the local copy is the main source the UI reads from, and the network is used to keep it in sync.

## Source
Captured from a working session on taking a small-team web app to native mobile (November 2026).

The name comes from HTTP caching. RFC 5861, "HTTP Cache-Control Extensions for Stale Content" (Mark Nottingham, May 2010), defines `stale-while-revalidate` and `stale-if-error`. Vercel's SWR React library (late 2019) brought the pattern into client-side data fetching, and TanStack Query uses the same model. "Offline First" as a design movement started with the Hoodie team's "Say Hello to Offline First" (Alex Feyerke, November 2013).

---

## Compass

**Roots** — *where this comes from*
It is a deliberate trade against [[Cache Invalidation]]: rather than trying to always be fresh, accept bounded staleness and refresh in the background. Its building blocks are [[In-Memory Caching]] and, in the browser, a [[Service Worker]].

**Paths** — *where this leads*
On the write side, the matching move is [[Optimistic UI]], showing the result before the server confirms it. When the background fetch fails, [[Graceful Degradation]] keeps the stale copy on screen instead of an error, which is RFC 5861's `stale-if-error`.

**Neighbors** — *what lives nearby*
It sits near [[Design Every UI State]], because "stale but refreshing" is a state that needs its own design, and [[Server-Authoritative State]], which says the local copy is a view of the server, never the source of truth.

**Clash** — *what pushes against this*
Stale data is wrong for some screens: balances, stock levels and anything someone will act on immediately. Unclear staleness also confuses users when numbers silently change. [[A Stale Source Is Confidently Wrong]] is the general warning, so mark or limit staleness where it matters.
