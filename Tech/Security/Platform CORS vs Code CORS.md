---
type: atomic
tags: [coding/security, coding/web-api, coding/azure, web, coding/dotnet]
date: 2026-10-01
---

# Platform CORS vs Code CORS

## Idea
Your hosting platform may have its own CORS switch sitting in front of your app. If it's turned on, it answers the browser before your code ever runs, and your carefully written CORS policy is silently ignored. Configure CORS in exactly one place.

## Definition
[[CORS]] is normally set in code, for example ASP.NET Core's CORS [[Middleware]] or Express's `cors` package. But many hosting platforms add their own CORS feature at a layer *in front of* the app: a setting in the portal or bucket config that inspects the `Origin` header and writes the `Access-Control-Allow-*` headers itself. When the platform setting has any allowed origins, it takes over. It answers the [[Preflight Request (OPTIONS)]] on its own, and the app's CORS headers are dropped or ignored, so changes to the code policy appear to do nothing. Origins added in code never get through, and credentialed requests fail if the platform's "allow credentials" flag is off. In other setups both layers write headers and the browser sees a duplicated `Access-Control-Allow-Origin` (for example, `https://app.example.com, https://app.example.com`), which it rejects as invalid even though both values are correct. The symptom looks identical to a missing CORS config, so people keep editing the wrong layer. The rule: pick one owner. Use the platform setting for static files or functions with no code of your own, and use code CORS (with the platform setting cleared) when you need per-route policies, credentials or anything dynamic. Better still, put the frontend and API behind one origin with [[Single Origin Ingress]] through an [[Edge Gateway]], and the browser never makes a cross-origin call, so CORS goes away.

## Providers
- **Azure** — [[Managed Web Hosting (PaaS)|App Service]] and [[Serverless Functions|Functions]] have a portal or `cors` site setting. Any entry there overrides the app's own CORS, so clear the list to let the code handle it.
- **AWS** — API Gateway has its own CORS config (HTTP APIs answer preflight at the gateway; with REST API proxy integrations the backend must still return the headers), and S3 buckets have a bucket CORS policy for direct browser access.
- **Google Cloud** — Cloud Storage bucket CORS configuration; API Gateway and Cloud Endpoints can pass CORS through to the backend or handle it at the proxy.
- **In code** — ASP.NET Core `AddCors`/`UseCors`, Express `cors`, FastAPI `CORSMiddleware`, Spring `@CrossOrigin`.

## Source
The CORS protocol is defined in the WHATWG Fetch Standard. The platform-layer CORS behaviour is documented separately by each host. Azure App Service's docs, for example, state that platform CORS and app CORS can't be used together.

---

## Compass

**Roots** — *where this comes from*
It follows directly from how [[CORS]] and the [[Preflight Request (OPTIONS)]] work: whichever layer answers the preflight first decides the outcome.

**Paths** — *where this leads*
The cleanest fix is architectural: [[Single Origin Ingress]] behind an [[Edge Gateway]] makes the frontend and API the same origin, so there's no CORS to configure anywhere.

**Neighbors** — *what lives nearby*
Same kind of bug as [[Path Base Stripping]]: a platform layer in front of your app quietly changes the request or response before your code sees it. On Windows hosting the layer is the [[IIS]] CORS module.

**Clash** — *what pushes against this*
Platform CORS isn't wrong. For a static bucket or a code-free function it's the only option and less work than middleware. The rule is "one owner", not "always in code", and moving to one origin trades CORS headaches for routing config on the gateway.
