---
type: atomic
tags: [frontend, web, coding/javascript, coding/security]
date: 2026-10-01
---

# Single-Page Application (SPA)

## Idea
Instead of the server sending a fresh page every time you click, the browser loads one page once and JavaScript redraws the screen itself. That makes the app feel instant, but it moves routing, rendering and sign-in into the browser, and each of those brings a cost.

## Definition
A single-page application serves one HTML file (usually `index.html`) plus a bundle of [[JavaScript]]. After that first load, clicking a link doesn't ask the server for a new page. JavaScript swaps the visible view and fetches only data, typically JSON from a [[REST API]]. **Client-side routing** changes the address bar with the browser's History API, so `/orders/42` is a view the app draws, not a file on the server. The classic gotcha comes from that: refresh or open a deep link and the server looks for a real `/orders/42` file and returns 404. The fix is a **rewrite rule** that sends every unknown path back to `index.html` so the app can route it. The costs: a heavier first load, and weaker SEO because crawlers may see an empty shell before scripts run (server-side rendering or prerendering helps). Security is the other catch. A SPA is a **public client**: all its code ships to the user, so it can't keep a client secret. It signs in with the **authorization code flow plus PKCE**, which proves the same app started and finished the login without needing a stored secret.

## Providers
- **Frameworks** — [[Angular]], React, Vue and Svelte all build SPAs; each ships a client-side router.
- **Azure** — Static Web Apps hosts the static bundle and supports a `navigationFallback` rewrite to `index.html`.
- **AWS** — Amplify Hosting, or S3 + CloudFront with a custom error response that maps 403/404 to `index.html`.
- **Google Cloud** — Firebase Hosting, with a `rewrites` rule sending `**` to `/index.html`.
- **Others** — Netlify (`_redirects` file) and Vercel (`rewrites` in `vercel.json`).

## Source
The term spread in the early 2000s alongside Ajax (XMLHttpRequest). PKCE for public clients is RFC 7636 (2015), and the OAuth 2.0 for Browser-Based Apps guidance from the IETF OAuth working group recommends it for SPAs.

---

## Compass

**Roots** — *where this comes from*
It is built from [[JavaScript]] (often written as [[TypeScript]]) that calls a [[REST API]], and frameworks like [[Angular]] exist to make that structure manageable.

**Paths** — *where this leads*
The fast-loading frame of a SPA is its [[App Shell]], and its sign-in runs through [[OAuth 2.0 and OIDC]] against an [[Identity Provider (IdP)]], in Angular usually via [[MSAL Authentication]].

**Neighbors** — *what lives nearby*
[[Runtime Config (Build Once Deploy Everywhere)]] lets one static bundle run in every environment. [[CORS]] decides whether the browser may call an API on another origin. [[Angular Route Guard]] protects client-side routes, but only for user experience, since the real check is on the server.

**Clash** — *what pushes against this*
For content-heavy or mostly static sites, a server-rendered or multi-page app is simpler, loads faster the first time and is crawled better. Shipping a large JavaScript bundle to show a page of text is a real cost.
