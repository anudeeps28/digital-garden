---
type: atomic
tags: [coding/security, coding/database]
date: 2026-10-04
---

# SECURITY DEFINER Functions

## Idea
A Postgres function marked SECURITY DEFINER runs with its owner's privileges, not the caller's. That lets it do things the caller can't, including skipping row-level policies, so it must be written like a tiny privileged API.

## Definition
By default PostgreSQL functions are `SECURITY INVOKER`: they run with the permissions of whoever calls them. **`SECURITY DEFINER`** flips that, much like a setuid program in Unix, so the body runs as the function's owner, often a role that bypasses [[Row-Level Security]]. It is the right tool when a narrow operation needs more privilege than the caller has. A worked example: a signup trigger that inserted a profile row for each new user needed it, because at that moment the request had no authenticated user id yet and RLS would have blocked the insert. The hardening checklist is short and important: set a fixed path with `SET search_path = public, pg_catalog` (or empty, with fully qualified names) so a caller can't shadow a function with their own, schema-qualify every table, validate and cap inputs, and `REVOKE EXECUTE ... FROM PUBLIC` then grant it only to roles that need it.

```sql
create function public.handle_new_user() returns trigger
language plpgsql security definer set search_path = public, pg_catalog as $$ ... $$;
```

## Source
Part of the SQL standard's routine security characteristic, and documented in the PostgreSQL manual under "Writing SECURITY DEFINER Functions Safely". The search_path risk got wide attention with CVE-2018-1058 (PostgreSQL, March 2018).

---

## Compass

**Roots** — *where this comes from*
It is a [[PostgreSQL]] feature borrowed from the setuid idea, and it most often shows up inside [[Database Triggers]] that must act before or regardless of the user's own rights.

**Paths** — *where this leads*
Each definer function becomes a privileged entry point, so it deserves the same review as a [[Service Role Key]] path and should run under an owner role shaped by [[Least-Privilege Database Roles]].

**Neighbors** — *what lives nearby*
It is the in-database counterpart of an app helper that checks membership and then acts with elevated rights, and [[Row-Level Security]] is the protection it can quietly bypass.

**Clash** — *what pushes against this*
It pushes against [[Defence in Depth]]: every definer function is a hole in RLS, so a sloppy one (no fixed search_path, unchecked input) can hand any caller the owner's full power.
