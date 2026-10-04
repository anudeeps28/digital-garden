---
type: atomic
tags: [frontend, web]
date: 2026-10-04
---

# Progressive Web App

## Idea
A Progressive Web App is a website that can be installed, work offline and send notifications, giving most of a native app's feel from one web codebase.

## Definition
A PWA is an ordinary web app plus three ingredients: served over HTTPS, a **web app manifest** (name, icons, colours, display mode) that lets the browser install it to the home screen, and a [[Service Worker]] that caches assets and data so it opens instantly and survives bad networks. "Progressive" means it works as a normal site everywhere and gains app-like powers where the browser supports them. The case for choosing it over a native app is strong for small teams and personal tools: one codebase, no app-store review, instant updates, and a link is the installer. The honest limits sit mostly on iOS: storage for sites not added to the home screen can be evicted after a period of non-use, [[Web Push]] works only once the app is installed to the home screen, and some device APIs are missing. Designing for those limits means keeping the server as the source of truth, treating local caches as disposable, and nudging iOS users to install.

## Source
Named in 2015 by Alex Russell and designer Frances Berriman ("Progressive Web Apps: Escaping Tabs Without Losing Our Soul"); promoted by Google from 2015-2016. Apple added service workers in Safari 11.1 (2018) and home-screen web push in iOS 16.4 (2023).

---

## Compass

**Roots** — *where this comes from*
It builds on the [[Single-Page Application (SPA)]] model and the [[App Shell]] pattern, where a cached shell loads instantly and content fills in afterward.

**Paths** — *where this leads*
Once the app runs offline, [[Optimistic UI]] and honest freshness indicators become necessary, and the [[Service Worker]] update lifecycle becomes a real deployment concern.

**Neighbors** — *what lives nearby*
[[Web Push]] is the notification channel, and [[Cache Invalidation]] is the hard problem that every offline cache eventually raises.

**Clash** — *what pushes against this*
Native apps still win on deep device access and on iOS reliability. If a feature must work every time on iPhone, a PWA's platform limits can turn into [[Silent Failure|silent failures]] the user never sees.
