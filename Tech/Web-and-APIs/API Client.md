---
type: atomic
tags: [coding/api, coding/testing, dev-tools]
date: 2026-10-03
---

# API Client

## Idea
An API client is a tool for talking to an API by hand: you build a request, send it, and look at exactly what comes back, with no app or browser in the way.

## Definition
An API client lets you put together a [[Request and Response|request]]: the URL, the [[HTTP Methods|method]] (GET, POST and so on), headers, a [[JSON]] body and any login token. You send it and see the raw response: the [[HTTP Status Codes|status code]], the headers and the body. It's the quickest way to answer "does the API itself work?" before blaming the frontend.

Most API clients add four things on top:
- **Collections**: saved requests grouped by API, so a whole set of calls can be rerun or shared with the team.
- **Environments**: variables such as `{{baseUrl}}` and `{{token}}` that swap between dev, test and prod without editing every request. Real secrets belong in the environment (or a [[Secrets and Key Management|secret store]]), never in a shared collection.
- **Auth helpers**: they fetch and attach tokens (OAuth 2.0, API keys, bearer tokens) so you don't paste them by hand.
- **Scripts and assertions**: small checks such as "status is 200" or "the body has an `id`" turn a saved request into a lightweight test. Collections can then run from the command line in a [[CI-CD Pipeline]].

Two things trip people up. First, an API client is not a browser, so browser-only rules such as [[CORS]] don't apply. A request can succeed in the client and still fail in the web app. Second, many clients can import a [[Swagger and OpenAPI|OpenAPI]] spec and generate a ready-made collection, which beats typing every endpoint by hand.

## Tools
- **Postman**: the best-known one. Desktop and web app, collections, environments, test scripts; `newman` or the Postman CLI runs collections in CI.
- **Insomnia** (Kong): similar feature set, with REST, GraphQL and gRPC.
- **Bruno**: open source; keeps collections as plain files in your repo so they're versioned with [[Git]].
- **Editor-based**: VS Code's REST Client and JetBrains' HTTP Client run requests from `.http` files; Thunder Client is a Postman-style VS Code extension.
- **Command line**: `curl` and HTTPie, scriptable and available everywhere.
- **Built into API docs**: Swagger UI's "Try it out" button is a minimal API client generated from the spec.

## Source
Postman Learning Center (learning.postman.com): "Collections", "Environments" and "Writing tests"; Bruno documentation (docs.usebruno.com) on file-based collections.

---

## Compass

**Roots** — *where this comes from*
It's a hands-on way to exercise a [[REST API]]: every concept in the API (methods, status codes, headers) is something you can poke at directly in the client.

**Paths** — *where this leads*
Saved collections with assertions grow into automated API tests, the same idea as [[Integration Tests]] but driven from outside the codebase. Running them in the pipeline catches a broken endpoint before users do.

**Neighbors** — *what lives nearby*
[[Swagger and OpenAPI]] describes the API, and the client calls it. Browser automation like [[Playwright]] tests the same backend through the UI instead.

**Clash** — *what pushes against this*
Collections kept in a separate app drift away from the code and quietly go stale. That's why file-based clients like Bruno, and tests written in the codebase itself, are gaining ground. A passing request in a client also proves nothing about browser-only behaviour like [[CORS]].
