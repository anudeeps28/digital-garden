---
type: atomic
tags: [coding/database, coding/security, sql]
date: 2026-09-16
---

# Least-Privilege Database Roles

## Idea
Most applications connect to their database as an account that can do anything, then rely on the code to never do the wrong thing. Give each component its own account that *can't*.

## Definition
Least-privilege database roles means every application component connects with a distinct database principal granted only the operations it actually performs, on only the objects it actually touches. The granularity that matters is **per schema, not per database**: granting `SELECT` on a schema and nothing else means a new table added to a different schema is inaccessible by default rather than accessible by accident. So a reporting component gets read on the reporting schema; a writer gets insert and update on its own schema and nothing on anyone else's. Combined with [[Managed Identity]] there are no passwords to rotate, and combined with [[Row-Level Security]] the account restriction and the row restriction fail independently — which is the whole point of [[Defence in Depth]].

## Source
The principle of least privilege, articulated by Saltzer and Schroeder in "The Protection of Information in Computer Systems" (1975), applied to database access control.

---

## Compass

**Roots** — *where this comes from*
It's the identity layer of [[Multi-Tenant Data Isolation]], and it presupposes a way to authenticate without secrets: [[Managed Identity]].

**Paths** — *where this leads*
Role definitions have to be created and kept in sync as schemas evolve, which makes them part of [[Database Migrations]] rather than a one-time manual setup.

**Neighbors** — *what lives nearby*
[[Read-Only by Default]] is the same instinct as a personal working habit; [[Authorization]] is the application-layer counterpart.

**Clash** — *what pushes against this*
Every new feature that crosses a schema boundary now needs a grant, and a missing grant surfaces as a runtime failure in production rather than a compile error. Convenience argues hard for one powerful account.
