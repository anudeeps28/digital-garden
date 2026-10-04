---
type: atomic
tags: [coding/security, web, coding/networking]
date: 2026-10-04
---

# Cross-Site WebSocket Hijacking

## Idea
Browsers don't apply CORS to WebSockets, so any web page you visit can open a socket to your server, including one on localhost. The server has to check who is knocking.

## Definition
**Cross-Site WebSocket Hijacking (CSWSH)** is cross-site request forgery for [[WebSocket]] connections. The handshake is an HTTP upgrade request that the browser sends with cookies attached, and the same-origin policy does not block it, so a malicious page can open `ws://127.0.0.1:PORT` or `wss://yourapp.com/socket`, ride the user's session, and then read and write messages in both directions. The defence is to check the `Origin` header at the upgrade handshake against an allowlist and reject everything else. A worked example: a local developer tool served a WebSocket on a loopback port; it rejected any handshake whose `Origin` wasn't its own page, and required a per-session token as a second factor, sent in the `Sec-WebSocket-Protocol` header rather than the query string so it never landed in access logs. The gate sits at the handshake, not on each message, because once the socket is open the attacker already has a live channel.

## Source
Named and described by security researcher Christian Schneider in a blog post on 31 August 2013. MITRE later catalogued it as CWE-1385, "Missing Origin Validation in WebSockets".

---

## Compass

**Roots** — *where this comes from*
It exists because [[CORS]] governs `fetch` and XHR but the WebSocket spec left origin checks to the server, so the protection you get for free on normal requests simply isn't there.

**Paths** — *where this leads*
The fix is a server-side form of [[Origin Verification]] at the handshake, and for anything on localhost you also need to defend against [[DNS Rebinding]], which can make an attacker's page look same-origin.

**Neighbors** — *what lives nearby*
It is a close relative of CSRF and of [[Cross-Site Scripting (XSS)]]: all three abuse the fact that the browser carries the user's ambient credentials for whoever asks.

**Clash** — *what pushes against this*
`Origin` is only meaningful from browsers; non-browser clients can send any value, so origin checks must sit alongside real [[Authentication]] rather than replace it.
