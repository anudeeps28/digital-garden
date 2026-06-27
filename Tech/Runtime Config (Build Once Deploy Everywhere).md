---
type: atomic
tags: [coding, angular, deployment, pattern]
date: 2026-04-02
---

# Runtime Config (Build Once, Deploy Everywhere)

## Idea
Load app settings from an external config file at runtime instead of baking them into the build — so one build works in every environment.

## Definition
Normally, frontend frameworks like Angular bake settings (API URLs, feature flags) into the code at **build time** using environment files (`environment.ts`, `environment.prod.ts`). This means you need a **separate build for each environment** — one for dev, one for test, one for prod — because each has different API URLs.

**The "build once, deploy everywhere" pattern** fixes this:
1. Build the Angular app **once** with a generic setup
2. Place a `config.json` file alongside the built app with environment-specific settings:
   ```json
   { "apiBaseUrl": "https://api-test.example.com" }
   ```
3. At startup, the app fetches `config.json` and loads the settings
4. To deploy to a different environment, just swap `config.json` — no rebuild needed

**In PlanDocumentRAG**, `ConfigService` loads `config.json` in the Angular app's `APP_INITIALIZER`:
```typescript
load(): Promise<void> {
    return firstValueFrom(
        this.http.get<Partial<AppConfig>>('config.json')  // relative path!
    ).then(cfg => { this.config = { ...this.config, ...cfg }; });
}
```

**Key lesson:** The path to `config.json` must be **relative** (no leading `/`). If the app is served from a subdirectory like `/rag/`, an absolute path `/config.json` goes to the root of the domain (404). A relative path `config.json` resolves to `/rag/config.json` — see [[Relative vs Absolute Paths]].

## Source
PlanDocumentRAG Angular app — blank page at `/rag/` because `config.json` was requested with absolute path. Fixed by removing the leading slash.

---

## Compass

**Neighbors** — *what lives nearby*
[[App Settings Override appsettings.json]] applies the same concept to backend .NET applications, while [[Connection String]] represents another environment-specific setting that varies per deployment. [[Docker]] containers likewise follow the "build once, run anywhere" philosophy, packaging a single image for deployment across different environments.

**Clash** — *what pushes against this*
Build-time configuration using `environment.ts` bakes settings directly into the code, requiring separate builds for each environment. Hard-coded URLs in source code similarly lock configuration to a single target.

**Roots** — *where this comes from*
[[CI-CD Pipeline]] embodies the principle of building once and deploying through pipeline stages, and [[Dependency Injection]] shares the same philosophy of decoupling configuration from code.

**Paths** — *where this leads*
[[Relative vs Absolute Paths]] becomes critical when the app runs in a subdirectory, and this pattern enables simpler CI/CD workflows where one build artifact flows seamlessly through dev → test → prod without rebuilding.
