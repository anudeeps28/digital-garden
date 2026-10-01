---
type: atomic
tags: [frontend, web, coding/javascript]
date: 2026-10-01
---

# JavaScript

## Idea
JavaScript is the one language every browser runs, so anything interactive on the web ends up as JavaScript, even code written in something else.

## Definition
JavaScript is a **dynamically typed** language: a variable can hold a number now and a string later, and type mistakes only show up when the code runs. It runs on a **single thread** with an **event loop**. There's one call stack, and slow work like network calls, timers and file reads is handed off. When that work finishes, its callback is queued and runs once the stack is free. This is why long synchronous loops freeze a page: nothing else can run until they finish. Asynchronous code is written with **promises** (an object standing for a value that will arrive later) and `async`/`await`, which makes promise-based code read top to bottom. Outside the browser, Node.js runs the same language on servers using the same event-loop model, which suits I/O-heavy APIs and is a poor fit for CPU-heavy work. [[TypeScript]] is a typed superset that compiles down to plain JavaScript. The browser only ever runs the JavaScript output, so types are checked while you build, not while the code runs. A practical gotcha: `==` converts types before comparing (`"0" == 0` is true), so use `===`.

## Providers
- **Engines** — V8 (Chrome, Edge, Node.js), SpiderMonkey (Firefox), JavaScriptCore (Safari).
- **Runtimes** — Node.js, Deno and Bun run JavaScript outside the browser.
- **Azure** — Azure Functions supports a Node.js runtime.
- **AWS** — Lambda supports Node.js runtimes.
- **Google Cloud** — Cloud Run functions supports Node.js.
- **Others** — Cloudflare Workers run JavaScript on V8 isolates at the edge.

## Source
Created by Brendan Eich at Netscape in 1995. Standardised as ECMAScript (ECMA-262) by Ecma International, first edition 1997. Promises and modules arrived in ES2015 and `async`/`await` in ES2017.

---

## Compass

**Roots** — *where this comes from*
It was born to make web pages interactive, and the event loop reflects that origin: a browser tab must never block while waiting for the network.

**Paths** — *where this leads*
It powers every [[Single-Page Application (SPA)]] and [[App Shell]]. On the server it runs [[Serverless Functions]] and APIs. [[TypeScript]] and frameworks like [[Angular]] are built on top of it.

**Neighbors** — *what lives nearby*
[[Async Await in CSharp]] uses the same `async`/`await` idea on a multi-threaded runtime. [[RxJS Observable]] models streams of async values where a promise models just one. [[JSON]] is JavaScript's object syntax turned into a data format.

**Clash** — *what pushes against this*
Dynamic typing lets whole classes of bugs reach production, which is the case for [[TypeScript]]. The single thread makes CPU-bound work a bottleneck that languages like [[Python]] with native extensions or [[CSharp]] handle more naturally.
