---
type: roadmap
tags: [tech/software, business/startup, checklist, building, framework]
date: 2026-11-04
---

# Product Build Checklist

Everything to think through before and while building a software or digital product. Copy this per product and tick things off.

It's long on purpose. Not every box applies to every product, but every box is a question worth answering out loud, even if the answer is "not yet". The [[#Quick version (minimum for any v1)|quick version]] at the bottom is the floor.

---

## 1. Product basics

- [ ] **Problem:** what pain does this solve, in one sentence?
- [ ] **User:** who exactly is it for?
- [ ] **Core action:** the one thing it must do really well.
- [ ] **MVP scope:** what's in v1, and what's explicitly *not*. Writing down the [[Explicit Non-Goals]] is half the work.
- [ ] **Success metric:** how will I know it's working? Pick one tied to the outcome, not a vanity number ([[Report the Outcome, Not the Metric]], [[Goodhart's Law]]).

## 2. Frontend (UI/UX)

- [ ] Key screens and user flows sketched.
- [ ] Framework chosen (e.g. [[React]], Next.js, [[Angular]], Blazor, mobile).
- [ ] Works on mobile and desktop.
- [ ] Empty states, loading states, error states designed ([[Design Every UI State]]).
- [ ] **Accessibility:** readable contrast, keyboard friendly, alt text.

## 3. Backend

- [ ] Language and framework chosen (e.g. .NET, [[Python]], Node).
- [ ] API design: what [[API Endpoints|endpoints]], what data goes in and out ([[REST API]], [[Swagger and OpenAPI]]).
- [ ] Input validation on every endpoint ([[Runtime Schema Validation]]).
- [ ] **Background jobs:** scheduled tasks ([[Cron]]), queues ([[Message Broker]]), long-running work.
- [ ] **Third-party APIs:** list them, and plan for when they go down ([[Graceful Degradation]], [[Exponential Backoff]]).

## 4. Data and storage

- [ ] **Database:** which one ([[PostgreSQL]], SQL Server, Cosmos, SQLite) and why.
- [ ] Data model / [[Database Tables|tables]] sketched.
- [ ] **File storage:** where uploads, images, docs live (Blob, S3, R2 — all [[Object Storage]]).
- [ ] **Caching:** anything that should be fast (Redis, CDN). Know how it gets cleared ([[Cache Invalidation]]).
- [ ] **Backups:** automatic, and a tested way to restore ([[Restore Drill]], [[RTO and RPO]]).
- [ ] **Data retention:** what I keep, for how long, and how users delete it.

## 5. Users and security

- [ ] **Auth:** how users sign in (email, Google, magic link) — [[Authentication]], [[OAuth 2.0 and OIDC]].
- [ ] **Permissions:** who can see and do what ([[Authorization]], [[Role-Based Access Control (RBAC)|roles]]).
- [ ] **Secrets:** API keys and passwords in a vault or env vars, never in code ([[Secrets and Key Management]]).
- [ ] HTTPS everywhere.
- [ ] [[Rate Limiting]] on public endpoints.
- [ ] Dependencies kept up to date.

## 6. Hosting and infrastructure

- [ ] Where it runs (Azure, Vercel, VPS, Railway, Fly) — [[Managed Web Hosting (PaaS)]] vs [[Virtual Machines]] vs [[Serverless Containers]].
- [ ] **Domain, DNS, SSL** set up.
- [ ] **Environments:** dev, staging, production kept separate ([[Release Stages]]).
- [ ] **Cost estimate:** monthly hosting + API spend, and cost per user ([[Unit Economics]]).
- [ ] What breaks at 10x users? Plan for it ([[Scalability-and-Load-Parameters]]).

## 7. Code and shipping

- [ ] **[[Git]]:** repo, [[Git Branches|branching strategy]], [[Pull Request|PR reviews]].
- [ ] **Testing:** [[Unit Tests]] + a few end-to-end tests of key flows ([[Playwright]]).
- [ ] **CI/CD:** tests and deploys run automatically on push ([[CI-CD Pipeline]]).
- [ ] Easy rollback if a deploy breaks ([[Make Every Deploy Reversible]]).
- [ ] **Docs:** README with setup, run, and deploy steps.

## 8. Running it in production

- [ ] **Error tracking** (e.g. Sentry, App Insights) — the enemy is the [[Silent Failure]].
- [ ] **Logs** you can search ([[Structured Logging]]).
- [ ] **Uptime alerts** so I know before users do ([[Health Probe]]).
- [ ] **Analytics:** what users do and where they drop off.

## 9. Money

- [ ] **Pricing model:** free, one-time, subscription, usage-based.
- [ ] **Payments:** Stripe or similar, plus refunds and failed payments.
- [ ] Invoices and receipts.

## 10. Communication

- [ ] **Transactional email:** sign-up, password reset, receipts.
- [ ] **Notifications:** email, push ([[Web Push]]), in-app.
- [ ] **Support:** a way for users to report bugs or ask for help.
- [ ] **Feedback loop:** how I hear what users want next.

## 11. Legal and privacy

- [ ] Privacy policy.
- [ ] Terms of service.
- [ ] Cookie consent, if needed.
- [ ] GDPR / CCPA basics if users are in those regions.

## 12. AI features (if any)

- [ ] Model choice and fallback model ([[Model Tiering]], [[Pin the Model Version]]).
- [ ] Prompts versioned like code ([[Prompt Engineering]]).
- [ ] **Evals:** a test set to check quality before changes ship ([[Evals]], [[LLM-as-a-Judge]]).
- [ ] [[Tokens|Token]] cost per user, with limits.
- [ ] Guardrails for bad input and bad output ([[Structured Output Validation]]).

## 13. Launch and growth

- [ ] **Distribution:** how people find it (content, SEO, community, ads) — [[Building in Public]] is the cheapest one.
- [ ] Landing page.
- [ ] Launch plan (where, when, who to tell).
- [ ] Onboarding: first 5 minutes of a new user's experience.

---

## Quick version (minimum for any v1)

[[First Make It Work, Then Make It Better]]. If time is short, this is the floor:

1. Problem + user defined
2. Core screens
3. Backend + database
4. Auth
5. Hosting + domain
6. Git + auto deploy
7. Error tracking + backups
8. Privacy policy

---

## Related

- [[AI Engineer Roadmap]] — the learning path behind section 12.
- [[Definition of Done]] — this checklist is a definition of done for a whole product.
- [[Approve the Foundation Before Polish]] — why sections 1–7 come before 9–13.
