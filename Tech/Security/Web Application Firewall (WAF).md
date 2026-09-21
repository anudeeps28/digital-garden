---
type: atomic
tags: [coding/security, security, devops, web]
date: 2026-09-16
---

# Web Application Firewall (WAF)

## Idea
A WAF is a bouncer reading the contents of each request at the door, turning away the patterns that are never legitimate before they reach your code.

## Definition
A Web Application Firewall inspects HTTP requests at the edge and blocks those matching known attack signatures — SQL injection, cross-site scripting, path traversal, known-bad bots. It runs **managed rule sets** curated by the vendor (Azure's Default Rule Set, AWS Managed Rules, the open OWASP Core Rule Set) plus custom rules you add. Two operational details matter more than the rules themselves. First, a WAF should start in *detection* mode so you can see what it would have blocked; switching straight to *prevention* mode without that soak period reliably breaks legitimate traffic. Second, managed rule sets are often gated to a higher pricing tier — see [[Tier-Gated Features]] — so a template that requests them on the cheap tier compiles cleanly and is rejected at deploy time.

## Source
Category formalized by the OWASP ModSecurity Core Rule Set (2006 onward); managed offerings from Azure Front Door, AWS WAF, and Cloudflare.

---

## Compass

**Roots** — *where this comes from*
A WAF only sees everything if everything goes through it — it presupposes [[Single Origin Ingress]].

**Paths** — *where this leads*
It's one layer: [[Origin Verification]] stops the bypass, [[Rate Limiting]] stops the volume, and input validation in the application stops what the rules missed.

**Neighbors** — *what lives nearby*
[[DOMPurify]] does the same pattern-matching job for markup on the client; a WAF does it for requests at the edge.

**Clash** — *what pushes against this*
Signature matching is inherently approximate: false positives on legitimate traffic, blind spots on novel attacks. It buys time, not correctness — it is no substitute for parameterized queries and output encoding.
