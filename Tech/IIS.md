---
type: atomic
tags: [#coding, #web-server, #iis, #microsoft]
date: 2026-04-02
---

# IIS (Internet Information Services)

## Idea
Microsoft's web server software — the receptionist that receives all incoming web requests before your app code runs.

## Definition
IIS is a web server built into Windows. It listens for incoming HTTP/HTTPS requests and routes them to the right application. Think of it like a receptionist at an office building — every visitor (request) goes through the receptionist first, who can check IDs, enforce rules, and then direct them to the right office (your code).

IIS has a **module pipeline** — a chain of small programs (modules) that each process the request before it reaches your app. The CORS module, authentication module, URL rewrite module, etc. all run in this pipeline. This is why IIS-level CORS settings can intercept preflight requests before your ASP.NET Core [[Middleware]] ever sees them.

**In-process vs Out-of-process hosting:**
- `hostingModel="inprocess"` — your app runs **inside** the IIS worker process (w3wp.exe). IIS modules and your middleware share the same pipeline. Faster, but IIS modules run first.
- `hostingModel="outofprocess"` — IIS just proxies requests to [[Kestrel]] (a lightweight .NET web server). More isolation.

**Locally** you use Kestrel directly (no IIS), which is why things like CORS work differently in dev vs production.

## Source
PlanDocumentRAG CORS troubleshooting — the IIS CorsModule was intercepting OPTIONS preflight requests before ASP.NET Core middleware could handle them.

---

## Compass

**Neighbors** — *what lives nearby*
[[Kestrel]] is .NET's built-in lightweight web server used in local development, while [[Nginx]] serves as the Linux equivalent of IIS for reverse proxying and load balancing. [[Apache]] is another popular web server found across Linux and cross-platform environments.

**Clash** — *what pushes against this*
[[Kestrel]] has no module pipeline — your middleware IS the pipeline — and self-hosted apps bypass the need for an external web server entirely.

**Roots** — *where this comes from*
[[Azure App Service]] runs IIS under the hood on Windows, and [[Middleware]] represents ASP.NET Core's equivalent of IIS modules, but operating at the application level rather than the server level.

**Paths** — *where this leads*
IIS modules can conflict with app-level middleware, as seen in [[Azure Portal CORS vs Code CORS]], and understanding the IIS [[CorsModule]] is separate from ASP.NET Core CORS middleware is crucial for debugging. Configuration of these modules happens through [[web.config]], where you can add or remove modules to control request processing.
