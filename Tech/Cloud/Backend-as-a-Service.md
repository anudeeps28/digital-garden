---
type: atomic
tags: [devops, coding/database, coding/architecture, web]
date: 2026-10-04
---

# Backend-as-a-Service

## Idea
A Backend-as-a-Service hands you a hosted database, sign-in, file storage and auto-generated APIs, so a small app can ship without writing a backend at all.

## Definition
A BaaS bundles the parts nearly every app rebuilds: a managed database, **auth** (email, magic links, OAuth providers), object storage, and APIs generated from the schema, often with realtime subscriptions on top. The client talks to it directly using a public key, and access is controlled by database rules such as [[Row-Level Security]] rather than by hand-written endpoints. For a tool with three users this is a huge win: zero auth code, zero API boilerplate, and a free tier. The trade-offs show up later. Free tiers often **pause projects after about a week of inactivity**, so a hobby app can be asleep when you finally open it. Business logic leaks into database policies, functions and triggers that are harder to test and version than ordinary code. And a privileged server key that bypasses the rules must be guarded carefully. A sound shape is to keep any server you do run **stateless**, with all durable state in the BaaS, so the server can be thrown away and rebuilt at will.

## Providers
- **Firebase** — Google; document database, auth, storage, hosting, cloud functions.
- **Supabase** — open-source, built on PostgreSQL with RLS, auth, storage and auto REST APIs.
- **Others** — AWS Amplify, Appwrite, PocketBase, and the revived open-source Parse Server.

## Source
The "mobile backend as a service" category emerged around 2011 with Parse, Kinvey and StackMob; Firebase launched in 2011 as a realtime database and was acquired by Google in 2014; Supabase launched in 2020 as an open-source alternative. Who first coined the term could not be verified.

---

## Compass

**Roots** — *where this comes from*
It packages a [[Relational Database]] or document store together with [[Authentication]] and [[Object Storage]], the three things almost every app needs before its first real feature.

**Paths** — *where this leads*
Using it safely means [[Row-Level Security]] on every table and treating the [[Service Role Key]] as a secret, while signup hooks are usually built with [[Database Triggers]].

**Neighbors** — *what lives nearby*
[[Database Auto-Pause]] is the idle behaviour free tiers apply, and [[Stateless Services]] is the matching design for any server you keep beside it.

**Clash** — *what pushes against this*
Vendor lock-in and logic hidden in policies push against it as the app grows, and a public-key client model is unforgiving: one table without a policy is a data leak, which is why [[Fail Closed]] defaults matter.
