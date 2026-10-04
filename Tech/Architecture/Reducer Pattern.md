---
type: atomic
tags: [coding/architecture, coding/patterns, frontend]
date: 2026-10-04
---

# Reducer Pattern

## Idea
A reducer is a pure function `(state, action) → newState`. All state changes go through it, so behaviour is predictable, testable and replayable.

## Definition
Instead of letting any code mutate state, you describe each change as an **action** (a plain object like `{type: "join", playerId}`) and write one function that takes the current state and an action and returns the next state. The reducer never edits the old state and never performs I/O; it just computes. That gives you several things for free: every transition can be unit-tested with plain data, any sequence of actions can be replayed to reproduce a bug, and the history of actions is a log of what happened. A useful convention is to **return the very same object when an action changes nothing** (an invalid move, a duplicate join). Then the caller can decide whether anything happened with a cheap identity check, `if (next !== prev) broadcast(next)`, instead of a deep comparison. On a server holding shared state, that single line decides whether to notify every client.

```js
function reduce(state, action) {
  if (action.type === "join" && !state.players.includes(action.id))
    return { ...state, players: [...state.players, action.id] };
  return state; // no-op: same reference
}
```

## Tools
- **Redux** — the popular JavaScript state container built around reducers.
- **React `useReducer`** — the same idea for component-local state.
- **Elm** — the language whose update function inspired the shape.

## Source
The name comes from functional programming's `reduce` (fold): state is a fold over the stream of actions. It was popularised in front-end work by Redux, created by Dan Abramov and Andrew Clark in 2015, which credits Flux and the Elm Architecture (Evan Czaplicki) as inspirations.

---

## Compass

**Roots** — *where this comes from*
A reducer is just [[Pure Functions]] applied to state transitions, and it is the core of [[React]] state management via Redux and `useReducer`.

**Paths** — *where this leads*
It is the natural heart of [[Server-Authoritative State]], and it is a textbook [[Functional Core, Imperative Shell]]: the reducer is the core, the socket handling and broadcasting are the shell.

**Neighbors** — *what lives nearby*
A [[Finite State Machine]] is a reducer with an explicit, closed set of states. Returning new objects instead of mutating echoes [[Read-Only by Default]].

**Clash** — *what pushes against this*
For small local state, actions and a reducer are ceremony; a plain variable or a signal such as [[Angular Signals]] is simpler. Copying state on every change can also get expensive for very large structures.
