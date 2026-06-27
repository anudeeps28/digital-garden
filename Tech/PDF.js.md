---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# PDF.js

## Idea
PDF.js (the `pdfjs-dist` package) is a pure-browser PDF rendering engine — it draws PDF pages onto a canvas with no plugin or server round-trip.

## Definition
Built by Mozilla, PDF.js parses and renders PDF files entirely in JavaScript, so a web app can display documents inline instead of forcing a download or relying on the browser's native viewer. In practice, this enables interactive document viewing in web applications — for example, a chat UI can embed PDF.js to display source documents inline, letting users click citations and see the exact pages referenced, closing the trust loop for document-grounded applications.

## Source
Mozilla, first released 2011 as an open-source JavaScript PDF renderer; initially developed to provide an alternative to closed-source PDF plugins and to enable PDF viewing in the browser without external dependencies.

---

## Compass

**Neighbors** — *what lives nearby*
Both [[Markdown Rendering Pipe]] and PDF.js turn raw content into something viewable in the chat UI. Like [[JSON]] parsing, PDF.js is a form of client-side parsing that takes a document format and makes it interactive.

**Clash** — *what pushes against this*
A plain download link or server-side PDF-to-image conversion offer no inline, interactive rendering — they're opposite approaches to the same problem.

**Roots** — *where this comes from*
PDF.js is integrated as a component within [[Angular]], the framework that hosts it in the larger application.

**Paths** — *where this leads*
Inline document viewing enables grounded, verifiable responses — users can see the source material that answers were based on. There's also a sibling concern in [[DOMPurify]] — both are about rendering untrusted content safely in the browser.
