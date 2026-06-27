---
type: atomic
tags: [coding, web, security, cors, browser]
date: 2026-04-02
---

# CORS (Cross-Origin Resource Sharing)

## Idea
A browser security rule that blocks websites from calling APIs on different domains — unless the API explicitly allows it.

## Definition
When your website is at `domain-A.com` and it tries to call an API at `domain-B.com`, the browser says "nope" by default. This is the **Same-Origin Policy** — a fundamental browser security feature that prevents malicious websites from making requests to your bank's API using your cookies.

CORS is the mechanism that **relaxes** this restriction. The API server can say "I allow requests from domain-A.com" by including the header `Access-Control-Allow-Origin: https://domain-A.com` in its responses.

**How it works for "complex" requests (POST with JSON, etc.):**
1. Browser sends a [[Preflight Request (OPTIONS)]] first — "Hey API, do you allow requests from this origin?"
2. API responds with CORS headers — "Yes, I allow these origins, methods, and headers"
3. Browser sends the actual request
4. If preflight fails → browser kills the request, you see the CORS error in console

**In ASP.NET Core**, CORS is configured as [[Middleware]]:
```csharp
builder.Services.AddCors(options => {
    options.AddDefaultPolicy(policy => {
        policy.WithOrigins("https://mysite.com")
              .AllowAnyHeader()
              .AllowAnyMethod();
    });
});
app.UseCors(); // must come before UseAuthentication/UseAuthorization
```

**Key gotchas:**
- Origin matching is **exact** — `https://foo.com` ≠ `https://foo.com/` (trailing slash)
- Middleware order matters — `UseCors()` must come before `UseAuthentication()` and `UseAuthorization()`
- On [[Azure App Service]], there's a separate IIS-level CORS that can conflict with your code — see [[Azure Portal CORS vs Code CORS]]

## Source
PlanDocumentRAG deployment — CORS blocked Angular UI at `kbasdev.keyfamily.local` from calling the API at `azurewebsites.net`.

---

## Roots — *where this comes from*
CORS is one of many browser security features that make up [[Web Security]]. It exists to answer a fundamental question: why does CORS only apply to browsers and not to tools like Postman or curl?

## Paths — *where this leads*
The [[Preflight Request (OPTIONS)]] is the "permission check" that browsers send before executing certain requests, and understanding CORS often reveals a deeper problem when deploying to [[Azure App Service]] — there's a two-system conflict between [[Azure Portal CORS vs Code CORS]] that must be resolved. Configuring CORS properly requires understanding how it fits within the broader [[Middleware]] pipeline in ASP.NET Core.

## Neighbors — *what lives nearby*
[[Authentication]] shares CORS's role as a security mechanism that gates access, though it operates at a different layer. At the network level, [[Firewall Rules]] provide similar access control but at a lower level than CORS, which operates strictly in the browser.

## Clash — *what pushes against this*
When the frontend and backend are on the same domain, no CORS headers are needed at all — same-origin requests bypass CORS entirely. Additionally, [[Server-to-server calls]] don't enforce CORS because it's a browser-only mechanism; backend services communicating with each other ignore these headers entirely.
