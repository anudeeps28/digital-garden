---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# SAS Token

## Idea
A SAS token is a signed URL that grants time-limited, narrowly-scoped access to a single blob without handing out your storage keys.

## Definition
A Shared Access Signature (SAS) is a query-string token appended to an Azure Storage URL that grants exactly the access you specify — which blob, which permissions (read-only), and an expiry time — without exposing the account key. In practice, SAS URLs enable secure, expiring downloads: the API generates a SAS link valid for a limited window (e.g., fifteen minutes) pointing at [[Azure Blob Storage]], after which the link is dead. It's a capability-style alternative to routing every byte through a service, and it leans on the same expiry mindset as a [[Bearer Token]].

## Source
Microsoft, introduced in Azure Storage as a foundational access control feature; formalized in the Azure Storage Services REST API specification (2012+).

---

## Neighbors — *what lives nearby*
Both [[Bearer Token]] and SAS tokens are short-lived, scoped credentials embedded in a request. [[Authorization]] is encoded right into a SAS URL itself — the token specifies exactly "what you may do."

## Clash — *what pushes against this*
A [[Connection String]] sits at the opposite end of the spectrum: it's a full, long-lived account access that grants broad permissions, whereas a SAS token is a narrow, expiring grant.

## Roots — *where this comes from*
[[Azure Blob Storage]] uses SAS as the standard way to scope access to individual blobs. The bigger question underneath is [[Authentication]] — how do you grant access to a resource without sharing the master key?

## Paths — *where this leads*
SAS tokens enable secure, expiring downloads from [[Azure Blob Storage]]. They also tie into [[Rate Limiting]] — issuing SAS links keeps heavy file transfers off the API itself, allowing clients to download directly from storage instead of routing every byte through the server.
