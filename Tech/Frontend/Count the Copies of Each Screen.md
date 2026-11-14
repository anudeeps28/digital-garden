---
type: atomic
tags: [tech/frontend, tech/mobile, tech/architecture]
date: 2026-11-14
---

# Count the Copies of Each Screen

## Idea
The real cost of supporting more platforms is how many copies of each screen you have to keep in sync, so a small team should pick its number of copies on purpose.

## Definition
The logic behind your screens can live once, on the server. The screens themselves get copied once per front-end technology, and every change to a shared screen is made once per copy. That gives three options:

| Approach | Copies of each screen | Feel |
|---|---|---|
| A native app per platform (Kotlin/Compose for Android, Swift/SwiftUI for Apple) plus web | 4–5 | Best everywhere |
| Web for desktop, one shared app for phones and tablets (e.g. Compose Multiplatform) | 2 | Native on Android, good on Apple |
| Web everywhere, installed as a PWA | 1 | Okay |

Big companies pick the first row because they have a team per platform. A small team usually starts at one copy and adds a second only when the app needs something a web page can't do, such as home-screen widgets or a truly native feel on touch screens. The gap between web and native is mostly on phones; on desktop with a mouse and keyboard, a web app is already good, and Electron is just a web page in a window. Wrapping a website in an app shell gets you nothing on Android, because an installed PWA already *is* that wrapper.

## Source
Captured from a working session on taking a small-team web app to native mobile (November 2026). The broader idea, that every extra client has a recurring cost and not just a one-off build cost, is behind the "write once, run anywhere" promise of cross-platform frameworks from Java to React Native (2015) to Flutter (2017), and behind the counter-argument that shared code still needs per-platform polish.

---

## Compass

**Roots** — *where this comes from*
It is [[Single Source of Truth]] applied to UI: every extra copy is a chance for the copies to drift apart, just as duplicated data does. It also extends [[Separation of Concerns]], since only the screens get copied if the logic stays behind one service layer.

**Paths** — *where this leads*
Adding a second copy usually pushes the backend from pages-call-code to an API, the stage-2 move in [[Modular Monolith]]. The one-copy option relies on [[Progressive Web App]], an [[App Shell]] and a [[Service Worker]], and on Android a native copy means [[Kotlin]].

**Neighbors** — *what lives nearby*
It sits near [[Design Tokens]], which reduce the cost of each copy by sharing visual decisions across platforms, and [[Stale-While-Revalidate]], which closes much of the "feels fast" gap that makes people want native in the first place.

**Clash** — *what pushes against this*
Copies are not the only cost. App-store review, signing and distribution are a fixed tax on every native copy, and some features can't be built at any number of copies without going native. Shared-UI frameworks also blur the count: one codebase can still need platform-specific fixes.
