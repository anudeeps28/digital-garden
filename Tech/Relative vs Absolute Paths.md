---
type: atomic
tags: [#coding, #web, #fundamentals, #paths]
date: 2026-04-02
---

# Relative vs Absolute Paths

## Idea
An absolute path starts from the root (`/file.txt`), a relative path starts from where you currently are (`file.txt`) — the leading slash changes everything.

## Definition
A **path** is the address to a file or resource. Two kinds:

**Absolute path** — starts with `/`, always resolves from the root:
- `/config.json` → `https://example.com/config.json` (always the root)
- `/images/logo.png` → `https://example.com/images/logo.png`
- Like saying "Go to 123 Main Street" — same destination no matter where you start

**Relative path** — no leading `/`, resolves from the current location:
- `config.json` → if you're at `/rag/`, resolves to `https://example.com/rag/config.json`
- `../styles.css` → go up one directory, then find `styles.css`
- Like saying "Go next door" — depends on where you currently are

**Why this matters in web apps:**
When an app is deployed to a **subdirectory** (virtual directory like `/rag/`), absolute paths break because they go to the root of the domain, not the app's root. Relative paths work because they resolve from wherever the app is.

| Path | App at `/` | App at `/rag/` |
|------|-----------|----------------|
| `/config.json` | `example.com/config.json` ✅ | `example.com/config.json` ❌ (wrong!) |
| `config.json` | `example.com/config.json` ✅ | `example.com/rag/config.json` ✅ |

**On the filesystem**, same concept:
- `C:\Users\Anudeep\file.txt` — absolute (full path from drive root)
- `.\file.txt` or `file.txt` — relative to current working directory

## Source
PlanDocumentRAG — Angular app at `/rag/` requested `/config.json` (absolute) → 404. Changed to `config.json` (relative) → resolved to `/rag/config.json` → worked.

---

## Compass

**Neighbors** — *what lives nearby*
[[URL routing]] is how web frameworks map paths to code, and the `base href` in HTML sets the base for relative URL resolution — both concepts work alongside path resolution to determine where resources live.

**Clash** — *what pushes against this*
Absolute and relative paths are the two contrasting approaches to addressing files and resources, each with different tradeoffs depending on deployment context.

**Roots** — *where this comes from*
[[Runtime Config (Build Once Deploy Everywhere)]] requires that config file paths be relative for subdirectory deploys; file systems and web servers both use this core concept of relative vs absolute addressing.

**Paths** — *where this leads*
Always use relative paths when your app might be deployed to a subdirectory, and configure tools like Angular to use `<base href="/rag/">` in `index.html` to properly resolve relative paths based on deployment location.
