---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# PDF.js

## Idea
PDF.js (the `pdfjs-dist` package) is a pure-browser PDF rendering engine — it draws PDF pages onto a canvas with no plugin or server round-trip.

## Definition
Built by Mozilla, PDF.js parses and renders PDF files entirely in JavaScript, so a web app can display documents inline instead of forcing a download or relying on the browser's native viewer. In the KBA AI-Doc-Ingestion project, the `PlanDocumentRAG.Web` Angular 19 chat UI uses `pdfjs-dist` inside its document-viewer component to show the source plan PDFs a chat answer was grounded in — letting a reviewer click a citation and see the exact page the LLM pulled from. This closes the trust loop for RAG: the answer comes from the [[REST API]], and PDF.js renders the underlying evidence right beside it.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
Both [[Markdown Rendering Pipe]] and PDF.js turn raw content into something viewable in the chat UI. Like [[JSON]] parsing, PDF.js is a form of client-side parsing that takes a document format and makes it interactive.

**Clash** — *what pushes against this*
A plain download link or server-side PDF-to-image conversion offer no inline, interactive rendering — they're opposite approaches to the same problem.

**Roots** — *where this comes from*
PDF.js is integrated as a component within [[Angular]], the framework that hosts it in the larger application.

**Paths** — *where this leads*
The viewer shows the source that the [[REST API]]'s answer cited, closing the loop on grounded responses. There's also a sibling concern in [[DOMPurify]] — both are about rendering untrusted content safely in the browser.
