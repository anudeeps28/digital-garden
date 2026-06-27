---
type: atomic
tags: [coding/angular, frontend, security]
date: 2026-06-26
---

# DOMPurify

## Idea
DOMPurify is an HTML-sanitization library that scrubs dangerous markup — scripts, event handlers, javascript: URLs — out of HTML before it's inserted into the page.

## Definition
When you render HTML that didn't come from your own trusted templates, you risk cross-site scripting (XSS): malicious markup running in the user's browser. DOMPurify parses the HTML and strips anything that could execute code, returning a safe string you can hand to the DOM. In the AI document ingestion project, the `PlanDocumentRAG.Web` Angular 19 chat UI runs LLM output through DOMPurify before display — the model's answer is untrusted text, and once it's converted from markdown to HTML it must be cleaned before binding into the view. It's the last line of defence in the [[Markdown Rendering Pipe]], working alongside `marked`. Conceptually it's a client-side analogue of validating input at the [[REST API]] boundary: never trust content you didn't author.

## Source
AI document ingestion project

---

## Compass

**Roots** — *where this comes from*
DOMPurify is part of the app's broader [[Authentication]] and security posture — a foundational principle that untrusted content demands verification.

**Paths** — *where this leads*
DOMPurify enables safe rendering of the LLM's markdown answer through the [[Markdown Rendering Pipe]], and addresses the same sibling concern as [[PDF.js]] — safely presenting untrusted source content without exposing the user to malicious code.

**Neighbors** — *what lives nearby*
DOMPurify is the sanitization step inside the [[Markdown Rendering Pipe]], and both it and [[Authorization]] share the same core principle: establishing and enforcing safety boundaries — one for content integrity, the other for access control.

**Clash** — *what pushes against this*
Binding raw HTML with `[innerHTML]` and no sanitization leaves the application wide open to XSS attacks, the exact vulnerability DOMPurify is designed to prevent.
