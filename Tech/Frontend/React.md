---
type: atomic
tags: [frontend, web, coding/patterns]
date: 2026-10-04
---

# React

## Idea
React builds interfaces from components that describe what the UI should look like for a given state, and re-renders when that state changes.

## Definition
React is a JavaScript library for building user interfaces. You write **components**, functions that take props and state and return a description of the UI (usually in JSX), and React works out the minimal DOM updates when state changes. Data flows one way, from parent to child, and changes flow back through callbacks. Since 2019, **hooks** (`useState`, `useEffect`, `useReducer`, `useContext`) hold state and side effects inside function components. React itself is deliberately narrow: routing, data fetching and global state come from the ecosystem or from frameworks like Next.js. A useful lesson for small apps is that you rarely need a state library. `useReducer` gives you a pure `(state, action) => newState` function you can unit test, and Context passes it down without prop drilling. That covers most of what Redux was adopted for, with no extra dependency. Reach for a dedicated store only when many distant components update the same state at high frequency.

## Source
Created by Jordan Walke at Facebook (now Meta), used in the News Feed in 2011 and open-sourced at JSConf US in May 2013. Hooks arrived in React 16.8 (February 2019).

---

## Compass

**Roots** — *where this comes from*
It is written in [[JavaScript]], usually with [[TypeScript]], and popularised the component-based [[Single-Page Application (SPA)]].

**Paths** — *where this leads*
`useReducer` is the [[Reducer Pattern]] in miniature, and keeping reducers as [[Pure Functions]] makes UI logic testable with [[Vitest]] without rendering anything.

**Neighbors** — *what lives nearby*
[[Angular]] is the batteries-included alternative with its own router, DI and forms, and [[Design Tokens]] are how a React component library stays visually consistent.

**Clash** — *what pushes against this*
Its flexibility means every team assembles a different stack, and effects (`useEffect`) are a common source of subtle bugs. Opinionated frameworks argue the freedom costs more than it gives.
