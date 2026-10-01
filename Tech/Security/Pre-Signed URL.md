---
aliases: ["tech/sas-token", "tech/security/sas-token"]
type: atomic
tags: [coding/security, api, coding/azure]
date: 2026-06-26
---

# Pre-Signed URL

## Idea
A pre-signed URL is a link that carries its own permission slip: time-limited, narrowly-scoped access to one file, without handing out your storage keys.

## Definition
A pre-signed URL is an ordinary storage URL with a signature appended in the query string. The server that holds the storage key signs a statement — *this file, read-only, until 10:15* — and anyone holding the resulting link can do exactly that and nothing more. Storage checks the signature on every request, so no account key ever leaves the server and the client never needs credentials of its own. In practice it enables secure, expiring downloads and uploads: the API checks the user is allowed the file, generates a link valid for a short window (say fifteen minutes), and the client then talks to storage directly, after which the link is dead. It's a capability-style alternative to routing every byte through your API, and it leans on the same expiry mindset as a [[Bearer Token]]. The catch is that a link is a bearer credential: whoever has it can use it until it expires, so keep windows short and scopes tight.

## Providers
- **Azure** — Shared Access Signature (SAS) tokens on Azure Storage; a *user delegation SAS* is signed with an Entra identity rather than the account key, and is the safer kind.
- **AWS** — S3 presigned URLs (SigV4).
- **Google Cloud** — Cloud Storage signed URLs.
- **Others** — Cloudflare R2 and MinIO presigned URLs (S3-compatible).

## Source
Introduced with Azure Storage Shared Access Signatures (2012) and S3 query-string authentication; now a standard feature of every object store.

---

## Compass

**Roots** — *where this comes from*
The question underneath is [[Authentication]]: how do you grant access to a resource without sharing the master key? The answer encodes [[Authorization]] directly in the link — the URL itself says what you may do.

**Paths** — *where this leads*
Handing out links keeps heavy file transfers off the API itself, which relieves [[Rate Limiting]] and server cost — clients download straight from storage.

**Neighbors** — *what lives nearby*
A [[Bearer Token]] is the same idea for APIs: a short-lived, scoped credential carried in the request.

**Clash** — *what pushes against this*
A [[Connection String]] sits at the opposite end: full, long-lived account access. And a pre-signed link can't be revoked early on most platforms short of rotating the key that signed it.
