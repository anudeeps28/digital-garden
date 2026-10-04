---
type: atomic
tags: [coding/security, web, frontend]
date: 2026-10-04
---

# Cross-Site Scripting (XSS)

## Idea
If text from someone else ends up in your page as HTML, it can run as code in your users' browsers. Treat every outside string as data, never as markup.

## Definition
**XSS** happens when untrusted input is rendered into a page without escaping, so a value like `<img src=x onerror=steal()>` executes with the victim's session. It comes in three flavours: **stored** (saved in your database and served to others), **reflected** (bounced back from a URL parameter), and **DOM-based** (client-side code writes input into `innerHTML`). The main defence is contextual output encoding, which modern template engines and frameworks do by default; the danger lies in the escape hatches like `|safe`, `Markup()`, `dangerouslySetInnerHTML` and `bypassSecurityTrustHtml`. A worked example: a dashboard displayed post and video titles scraped from third-party sites; those titles are attacker-controlled, so the rule was to rely on template autoescaping and forbid ever marking a scraped string as safe. Where rich HTML is truly needed, run it through a sanitizer and add a Content-Security-Policy as a second layer.

## Source
The name "cross-site scripting" was coined by Microsoft security engineers in January 2000, and CERT published advisory CA-2000-02 on it in February 2000. It is part of A03 Injection in the OWASP Top 10 2021.

---

## Compass

**Roots** — *where this comes from*
It is an injection flaw born from mixing data and code in one channel, the same root cause as SQL injection, and a reason to treat all external content as untrusted input.

**Paths** — *where this leads*
When you must render user HTML, a sanitizer like [[DOMPurify]] belongs at the boundary, which is exactly what a [[Markdown Rendering Pipe]] should do before handing output to the page.

**Neighbors** — *what lives nearby*
[[Cross-Site WebSocket Hijacking]] and CSRF also ride the user's ambient session, and XSS is the main way tokens from [[PKCE]] flows get stolen out of browser storage.

**Clash** — *what pushes against this*
No single control is enough: autoescaping misses attribute and URL contexts, sanitizers have bypasses, and CSP is often loosened to `unsafe-inline`, so XSS is a standing argument for [[Defence in Depth]].
