---
type: atomic
tags: [frontend, web]
date: 2026-10-04
---

# Service Worker

## Idea
A service worker is a script the browser runs between your page and the network, able to cache, intercept requests and wake up for push, and its update lifecycle is the part that bites.

## Definition
A service worker is registered by a page and then lives independently of it. It can intercept every `fetch` from its scope and answer from a cache, which is what makes offline apps and instant loads possible, and it is woken for [[Web Push]] messages. Its lifecycle is **install → waiting → activate**. A new version installs in the background but then *waits* until every tab using the old one closes, so users can sit on a stale build for days. The tempting fix is to auto-update silently (`skipWaiting` plus a reload), but that can reload the page while someone is halfway through a form and wipe their input. The safer pattern is **prompt-to-update**: detect the waiting worker, show "A new version is ready, reload?", and only call `skipWaiting` after the user confirms. Two more rules: serve `sw.js` itself with `Cache-Control: no-cache` so the browser actually sees new versions, and version caches so old entries are deleted on activate.

## Tools
- **Workbox** — Google's library for caching strategies and precaching.
- **vite-plugin-pwa** — generates the worker and offers both `prompt` and `autoUpdate` modes.

## Source
Spec started in 2013-2014 by Alex Russell and Jake Archibald at Google as a replacement for the HTML5 AppCache; first draft May 2014; shipped in Chrome 40 (2015). Now a W3C specification.

---

## Compass

**Roots** — *where this comes from*
It replaced the brittle AppCache and is the engine behind the [[Progressive Web App]] and the [[App Shell]] pattern.

**Paths** — *where this leads*
Every caching decision it makes is a [[Cache Invalidation]] decision, and the update prompt is a small piece of [[Optimistic UI]] honesty about which version the user is running.

**Neighbors** — *what lives nearby*
It sits in the same spot as [[Middleware]] on a server, intercepting requests on their way through, and works with [[Runtime Config (Build Once Deploy Everywhere)]] when config must not be cached forever.

**Clash** — *what pushes against this*
A worker can serve a broken build long after you fixed it, so aggressive caching clashes with fast rollback. Debugging it is also harder than debugging the page, because it outlives tabs and deploys.
