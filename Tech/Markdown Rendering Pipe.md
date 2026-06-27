---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# Markdown Rendering Pipe

## Idea
A custom Angular pipe that takes the LLM's markdown answer and turns it into safe, displayable HTML — parsing with marked and sanitizing with DOMPurify.

## Definition
An Angular pipe is a small transform you apply in a template (`{{ answer | markdown }}`) to reshape a value for display. The markdown rendering pipe in the KBA AI-Doc-Ingestion project's `PlanDocumentRAG.Web` Angular 19 chat UI does two steps: first it runs the model's markdown through `marked` to produce HTML (so headings, lists, bold, and code blocks render properly), then it passes that HTML through [[DOMPurify]] to strip any XSS vectors before binding it into the DOM. The input is the answer text returned by the [[REST API]] — untrusted, since an LLM generated it — which is exactly why sanitization is non-negotiable. The result is then rendered via `[innerHTML]` in the chat bubble.

## Source
KBA AI Document Ingestion project

---

## Neighbors — *what lives nearby*
[[DOMPurify]] handles the sanitization side of this pattern, and [[PDF.js]] similarly transforms raw content (in PDF format) into something safely viewable in the browser.

## Clash — *what pushes against this*
You could display the raw markdown string as-is, which keeps the text readable but leaves formatting symbols like `**` and `#` showing literally on screen rather than rendering as bold or headings.

## Roots — *where this comes from*
[[Angular]] treats pipes as a core templating feature of the framework, making them the natural place to apply transformations like this right before display.

## Paths — *where this leads*
This pipe enables [[DOMPurify|DOMPurify's]] XSS-safety guarantee on markdown content, and it consumes answers that the [[REST API]] has streamed back from the model.
