---
type: atomic
tags: [devops, coding/architecture]
date: 2026-10-04
---

# Multi-Stage Docker Build

## Idea
Build your app in one throwaway image with all the heavy tools, then copy only the finished output into a small, clean runtime image.

## Definition
A multi-stage Dockerfile has several `FROM` lines. Each starts a new stage, and a later stage can pull files from an earlier one with `COPY --from=<stage>`. Only the last stage becomes the shipped [[Docker Image]]. A typical full-stack example: a `node` stage installs dependencies and builds the [[Single-Page Application (SPA)]] into `dist/`; the final stage starts from `python:slim`, installs only the API's runtime dependencies, and copies `dist/` in to be served as static files. Compilers, dev dependencies and source maps never reach production, so the image is smaller, faster to pull, and has less attack surface. `COPY --from` also works with any public image, which is a neat way to grab a single tool binary (for example a database client or a static binary from its official image) without installing a package manager. Finish with a `HEALTHCHECK` instruction so the runtime knows when the container is actually ready. Ordering layers from least to most frequently changed keeps rebuilds fast.

```dockerfile
FROM node:20 AS web
WORKDIR /web
COPY web/ .
RUN npm ci && npm run build

FROM python:3.12-slim
COPY --from=web /web/dist /app/static
HEALTHCHECK CMD curl -f http://localhost:8000/health || exit 1
```

## Source
Introduced in Docker 17.05 (May 2017), replacing the earlier "builder pattern" of two separate Dockerfiles and a shell script.

---

## Compass

**Roots** — *where this comes from*
It refines how a [[Docker Image]] is built with [[Docker]], separating build-time needs from run-time needs.

**Paths** — *where this leads*
The `HEALTHCHECK` feeds the same idea as a [[Health Probe]], and one image per commit supports [[Runtime Config (Build Once Deploy Everywhere)]].

**Neighbors** — *what lives nearby*
[[Build Artifacts]] in a [[CI-CD Pipeline]] follow the same split between building and shipping, and [[Docker Compose]] is usually what runs the result.

**Clash** — *what pushes against this*
Copying from a public image by tag trusts that image, so pinning by digest matters, and multi-stage files get hard to read once they pass four or five stages.
