---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# Markdown Rendering Pipe

## Idea
A custom Angular pipe that takes the LLM's markdown answer and turns it into safe, displayable HTML — parsing with marked and sanitizing with DOMPurify.

## Definition
An Angular pipe is a small transform you apply in a template (`{{ answer | markdown }}`) to reshape a value for display. A markdown rendering pipe follows two steps: first it runs markdown source through a parser like `marked` to produce HTML (so headings, lists, bold, and code blocks render properly), then it passes that HTML through [[DOMPurify]] to strip any XSS vectors before binding it into the DOM. The input is typically untrusted content — whether from user submissions, external APIs, or LLM responses — which is exactly why sanitization is non-negotiable. The result is then rendered via `[innerHTML]` binding in the template.

## Source
Angular pipes are a core templating feature documented in the Angular framework documentation; the pattern of combining markdown parsing (via libraries like marked) with HTML sanitization (DOMPurify) is a standard practice in web applications handling user-generated or untrusted content.

---

## Neighbors — *what lives nearby*
[[DOMPurify]] handles the sanitization side of this pattern, and [[PDF.js]] similarly transforms raw content (in PDF format) into something safely viewable in the browser.

## Clash — *what pushes against this*
You could display the raw markdown string as-is, which keeps the text readable but leaves formatting symbols like `**` and `#` showing literally on screen rather than rendering as bold or headings.

## Roots — *where this comes from*
This pattern emerges from the need to safely render dynamic content in the browser. [[Angular]] provides pipes as a templating feature specifically designed for in-template transformations, making them the natural place to apply a chain of sanitization steps right before display.

## Paths — *where this leads*
This pattern enables [[DOMPurify|DOMPurify's]] XSS-safety guarantee on any markdown content that flows through it — whether from user input, API responses, or generated text. It sits at the critical junction where untrusted data meets the DOM.
