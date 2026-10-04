---
type: atomic
tags: [coding/security, coding/web-api, api]
date: 2026-10-04
---

# IDOR (Insecure Direct Object Reference)

## Idea
If an endpoint fetches a record just because the caller asked for its id, anyone can read anyone else's data by changing a number in the URL. Knowing an id must never be the same as being allowed to use it.

## Definition
An **insecure direct object reference** happens when an API exposes an internal identifier (`/invoices/1042`, `?file=report.pdf`) and trusts it without checking that the caller owns or may access that object. The user is logged in, so [[Authentication]] passes, but the per-object [[Authorization]] check is missing. The fix is to scope every lookup to the caller: query by id **and** by the caller's tenant or user, so a foreign id simply returns "not found". Unguessable ids (UUIDs) slow attackers down but are not a fix. A worked example: an endpoint that issues download links looked up the file row by id together with the caller's tenant scope, confirmed membership before signing anything, and only ever signed the path stored in the database, never a path sent by the client. That last rule also shuts the door on [[Path Traversal]], because the client never gets to name a location.

## Source
OWASP introduced "Insecure Direct Object Reference" as its own category in the OWASP Top 10 2007 (A4). In 2017 it merged with Missing Function Level Access Control into Broken Access Control, which became A01, the top risk, in the 2021 list. The OWASP API Security Top 10 calls the same flaw BOLA (Broken Object Level Authorization).

---

## Compass

**Roots** — *where this comes from*
IDOR is what you get when [[Authorization]] is checked at the route level but not at the object level, and in a SaaS app it is the most common way [[Multi-Tenant Data Isolation]] quietly breaks.

**Paths** — *where this leads*
The durable fix is to make the caller's scope part of every query, resolved once by [[Tenant Resolution]] and enforced in the database by [[Row-Level Security]] as a backstop, so a forgotten check fails safe instead of leaking.

**Neighbors** — *what lives nearby*
A [[Pre-Signed URL]] endpoint is a classic IDOR trap, since it turns an unchecked id into a working download link, and [[Path Traversal]] is its filesystem cousin where the client-supplied reference is a path rather than an id.

**Clash** — *what pushes against this*
A [[Capability URL]] deliberately makes "knowing the reference" the permission, which is fine for low-stakes sharing but is exactly the model IDOR warns against for private data.
