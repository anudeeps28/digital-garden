---
type: atomic
tags: [#coding, #web, #cors, #http]
date: 2026-04-02
---

# Preflight Request (OPTIONS)

## Idea
A "permission check" that browsers automatically send before making cross-origin requests, asking the server "will you accept this?"

## Definition
When a browser needs to make a "complex" cross-origin request (like a POST with JSON body, or a request with custom headers), it doesn't just send it. First, it sends a lightweight **OPTIONS** request called a "preflight" — asking the server for permission.

**What the browser asks (OPTIONS request):**
- `Origin: https://mysite.com` — "I'm coming from here"
- `Access-Control-Request-Method: POST` — "I want to do a POST"
- `Access-Control-Request-Headers: Content-Type` — "I'll send these headers"

**What the server must respond with:**
- `Access-Control-Allow-Origin: https://mysite.com` — "Yes, I accept your origin"
- `Access-Control-Allow-Methods: POST, GET` — "These methods are OK"
- `Access-Control-Allow-Headers: Content-Type` — "These headers are OK"

If **any** of these response headers are missing, the browser kills the request. You see the error: *"Response to preflight request doesn't pass access control check"*.

**"Simple" requests skip preflight** — basic GET/POST with standard headers (like form submissions) don't trigger a preflight. But most API calls with JSON bodies do.

**Important:** The OPTIONS request has no authentication token. If your auth middleware runs before CORS middleware and rejects unauthenticated requests, it will reject the preflight → CORS fails. This is why `UseCors()` must come before `UseAuthentication()` in [[Middleware]] order.

## Source
PlanDocumentRAG CORS error — browser console showed "Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource."

---

## Compass

**Neighbors** — *what lives nearby*
[[HTTP Methods]] include OPTIONS alongside GET, POST, PUT, and DELETE. DNS lookup is another "pre-check" that happens before the real request, similar in spirit to how preflight validates whether a request should proceed.

**Clash** — *what pushes against this*
Same-origin requests don't need a preflight at all, and "simple" cross-origin requests (basic GET/POST with standard content types) skip the preflight check entirely.

**Roots** — *where this comes from*
[[CORS]] is the broader security mechanism that uses preflight as its permission-checking tool. The fundamental question underneath is: why does the browser check at all instead of just letting the server reject the request?

**Paths** — *where this leads*
Understanding preflight reveals why [[Azure Portal CORS vs Code CORS]] works differently—IIS can intercept the preflight before your application code runs. It also shows why [[Middleware]] pipeline ordering matters so much: who handles the preflight determines whether CORS succeeds or fails.
