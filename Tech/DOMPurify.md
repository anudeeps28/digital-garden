---
type: atomic
tags: [coding/angular, frontend, security]
date: 2026-06-26
---

# DOMPurify

## Idea
DOMPurify is an HTML-sanitization library that scrubs dangerous markup — scripts, event handlers, javascript: URLs — out of HTML before it's inserted into the page.

## Definition
When you render HTML that didn't come from your own trusted templates, you risk cross-site scripting (XSS): malicious markup running in the user's browser. DOMPurify parses the HTML and strips anything that could execute code, returning a safe string you can hand to the DOM. In practice, when untrusted content is converted from markdown to HTML, it must be sanitized before binding into the view. It's a critical layer of defense in HTML rendering pipelines, working alongside other sanitization tools. Conceptually it's a client-side analogue of validating input at system boundaries: never trust content you didn't author.

## Source
Cure53 (Mario Heiderich), first released 2013; widely adopted as the de facto standard for HTML sanitization in web applications.

---

## Compass

**Roots** — *where this comes from*
DOMPurify is part of the app's broader [[Authentication]] and security posture — a foundational principle that untrusted content demands verification.

**Paths** — *where this leads*
DOMPurify enables safe rendering of untrusted markup in templates and pipelines, and addresses the same sibling concern as [[PDF.js]] — safely presenting untrusted source content without exposing the user to malicious code.

**Neighbors** — *what lives nearby*
DOMPurify is a sanitization step in HTML rendering pipelines, and both it and [[Authorization]] share the same core principle: establishing and enforcing safety boundaries — one for content integrity, the other for access control.

**Clash** — *what pushes against this*
Binding raw HTML with `[innerHTML]` and no sanitization leaves the application wide open to XSS attacks, the exact vulnerability DOMPurify is designed to prevent.
