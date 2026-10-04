---
type: atomic
tags: [coding/security, web]
date: 2026-10-04
---

# Capability URL

## Idea
A capability URL is a link where holding the link is the permission. No login: if you have the unguessable URL, you're in.

## Definition
A **capability URL** embeds a long random token in the address (`/room/k7Qx...`, an "anyone with the link" document, a password-reset link) so that possession alone grants access. It trades identity for unguessability: the token must carry enough entropy (128 bits is a common floor) and be generated with a cryptographically secure source. A worked example: a two-person shared-room app had no accounts at all; creating a room produced an id from `crypto.getRandomValues`, the server validated incoming ids against a strict regex before touching storage, and sharing the link was how you invited someone. The risk is leakage, since URLs end up in browser history, server logs, `Referer` headers, chat previews and screenshots. Good practice is HTTPS only, `Referrer-Policy: no-referrer`, `noindex`, letting the owner revoke or rotate the link, and expiring it where the use case allows.

## Source
The capability idea comes from Dennis and Van Horn's 1966 paper on capabilities in operating systems. For the web, the W3C TAG's "Good Practices for Capability URLs" (edited by Jeni Tennison, first draft February 2014) set out the patterns and the leakage risks.

---

## Compass

**Roots** — *where this comes from*
It folds [[Authentication]] and [[Authorization]] into a single secret, which is why it feels so frictionless and why it has to be treated with the same care as a password.

**Paths** — *where this leads*
Anything that accepts the token should validate its shape before use, in the spirit of [[Runtime Schema Validation]], and should never let the token double as a file path, or you invite [[Path Traversal]].

**Neighbors** — *what lives nearby*
A [[Pre-Signed URL]] is the short-lived, server-issued sibling: same "the link is the key" model, but scoped to one object and expiring in minutes rather than living until revoked.

**Clash** — *what pushes against this*
For private per-user data this is the very pattern [[IDOR (Insecure Direct Object Reference)|IDOR]] warns against, and it sits awkwardly with [[Zero Trust]], which wants every request tied to a verified identity rather than a bearer secret.
