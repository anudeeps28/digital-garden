---
type: atomic
tags: [coding/database, coding/patterns]
date: 2026-10-04
---

# Database Triggers

## Idea
A trigger is code the database runs automatically when rows are inserted, updated or deleted, so a rule holds no matter which client made the change.

## Definition
A trigger attaches a function to a table event, `BEFORE` or `AFTER` an `INSERT`, `UPDATE` or `DELETE`, either once per row or once per statement. Inside, the function sees the `OLD` and `NEW` row and can modify it, reject it, or write to other tables. Common uses are audit logs, keeping `updated_at` current, maintaining derived columns, and setup work on new records. A classic case in hosted backends: when a user signs up, a trigger on the auth users table **creates a profile row** and seeds starter data, so no client ever has to remember to. The lesson there is about failure. If the seeding step throws, the whole signup transaction rolls back and the user cannot create an account at all. Wrapping the optional seeding in an exception handler (`BEGIN ... EXCEPTION WHEN OTHERS THEN ...`) that logs and continues means a failed seed never blocks signup. That is a deliberate trade: core work fails loudly, optional extras degrade gracefully. Because triggers on auth tables usually need elevated rights, they run as the function owner, which deserves care.

```sql
create trigger on_signup after insert on auth.users
for each row execute function public.handle_new_user();
```

## Source
Triggers appeared in commercial databases in the late 1980s (Sybase, Oracle 7 in 1992) and were standardised in SQL:1999. PostgreSQL has supported them since 1997, using a trigger function rather than inline SQL.

---

## Compass

**Roots** — *where this comes from*
They are a feature of the [[Relational Database]], in [[PostgreSQL]] written as functions, and they keep invariants at the data layer like a [[Foreign Key]] does.

**Paths** — *where this leads*
Triggers that touch protected tables are usually [[SECURITY DEFINER Functions]], and they are a common building block in [[Backend-as-a-Service]] apps.

**Neighbors** — *what lives nearby*
The exception wrapper is [[Graceful Degradation]] inside the database, and an [[Outbox Pattern]] often uses triggers to record events alongside writes.

**Clash** — *what pushes against this*
Swallowing errors pushes against [[Fail Fast Fail Loudly]], so it must be a conscious choice with logging. Triggers are also invisible from application code, which makes behaviour surprising and hard to test.
