---
type: atomic
tags: [frontend, web, coding/architecture, coding/angular]
date: 2026-10-01
---

# App Shell

## Idea
Load the frame first and the content after. The shell (header, navigation, layout, sign-in) appears instantly and stays the same, so the user sees a working app while the data is still on its way.

## Definition
The **app shell** is the minimal HTML, CSS and [[JavaScript]] needed to draw an app's chrome: the header, navigation, page layout and the sign-in flow. It contains no user data. Because it rarely changes, it can be cached aggressively, often by a **service worker** that serves it from the device on repeat visits, so the frame paints immediately and even works offline. Content is then fetched and placed into the shell's slots. The term has a second, related meaning in **micro-frontends**: a host "shell" application that owns the layout, routing and authentication, then loads separately built and deployed feature apps (**remotes**) into itself at runtime. In that setup the shell is the one place that knows who the user is. That's why separate products or portals usually each get their own shell, with their own sign-in flow and sometimes their own identity directory. The gotcha is version skew: a cached shell can outlive the content or remotes it expects, so cache-busting and shared-dependency versions need deliberate handling.

## Providers
- **Angular** — the root app component plays the shell role in a normal app. For micro-frontends, Native Federation (`@angular-architects/native-federation`) loads remotes into a host.
- **webpack** — Module Federation (webpack 5) lets a host load code from separately deployed remotes at runtime.
- **single-spa** — a framework-agnostic router that mounts and unmounts micro-frontends inside a root config.
- **PWA tooling** — service workers via Workbox precache the shell for instant repeat loads and offline use.
- **Google** — the "App Shell model" guidance for Progressive Web Apps, which named the pattern.

## Source
Google's Progressive Web App guidance (Chrome team, around 2015–2016) introduced the App Shell model. The micro-frontend sense comes from the micro-frontends idea popularised by ThoughtWorks Technology Radar (2016) and Webpack 5 Module Federation (2020).

---

## Compass

**Roots** — *where this comes from*
It's the loading strategy of a [[Single-Page Application (SPA)]]: separate what never changes from what always changes.

**Paths** — *where this leads*
Owning sign-in puts the shell in charge of [[OAuth 2.0 and OIDC]] against an [[Identity Provider (IdP)]], often via [[MSAL Authentication]]. In multi-product setups, [[Tenant Resolution]] decides which shell and directory a user lands in.

**Neighbors** — *what lives nearby*
[[Cache Invalidation]] is the hard part of caching a shell. [[Runtime Config (Build Once Deploy Everywhere)]] and [[APP_INITIALIZER]] load settings before the shell finishes booting. [[Standalone Components]] make Angular remotes easier to load lazily.

**Clash** — *what pushes against this*
Micro-frontend shells add real coordination cost: shared dependency versions, cross-app routing and duplicated bundles. For one team building one product, a single app is simpler.
