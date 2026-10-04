---
type: atomic
tags: [coding/security, coding/database, api]
date: 2026-10-04
---

# Service Role Key

## Idea
A service role key is a backend credential that skips the database's row-level rules. The moment you use it, your app code becomes the only thing standing between users and each other's data.

## Definition
Backend-as-a-service platforms usually hand out two keys: a **public (anon) key** that is safe in the browser because every query it makes is filtered by [[Row-Level Security]], and a **service role key** for trusted servers that bypasses those policies entirely. It is convenient for admin jobs, webhooks and server routes that need to cross users. The catch is that it inverts where security lives. With the public key, the database enforces access; with the service key, the database trusts you completely, so every route has to check membership and ownership itself. A worked example: a backend that used the service key for all queries routed each request through small `require_member` and `require_owner` helpers before touching data, kept RLS policies in place only as a backstop, and treated that helper module as the single most important file to review. The key must never reach a client bundle or a public repo.

## Providers
- **Supabase** — `service_role` key (newer "secret" keys) bypasses RLS.
- **Firebase** — Admin SDK credentials bypass Security Rules.

## Source
The two-key model is documented by Supabase (`anon` and `service_role` keys, built on PostgreSQL roles and RLS); Firebase's Admin SDK, which bypasses Security Rules, follows the same pattern.

---

## Compass

**Roots** — *where this comes from*
It grows out of the [[Backend-as-a-Service]] model, where the database is exposed directly to clients and [[Row-Level Security]] is the main gate, so a key that skips RLS is a deliberate hole in that gate.

**Paths** — *where this leads*
Once you hold it, [[Authorization]] moves into application code, and the service key belongs in [[Secrets and Key Management]] alongside any other root credential.

**Neighbors** — *what lives nearby*
[[Least-Privilege Database Roles]] offers the alternative of narrower roles per job, and [[SECURITY DEFINER Functions]] are the in-database version of the same "run with more power than the caller" trade-off.

**Clash** — *what pushes against this*
In the terms of [[Security Control vs Security Boundary]], RLS stops being the boundary and becomes a control you are bypassing, so a single missing check in app code is a full data leak.
