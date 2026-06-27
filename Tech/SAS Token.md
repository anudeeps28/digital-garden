---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# SAS Token

## Idea
A SAS token is a signed URL that grants time-limited, narrowly-scoped access to a single blob without handing out your storage keys.

## Definition
A Shared Access Signature (SAS) is a query-string token appended to an Azure Storage URL that grants exactly the access you specify — which blob, which permissions (read-only), and an expiry time — without exposing the account key. In the KBA AI Document Ingestion project I generate SAS URLs for secure, expiring downloads: when a user requests a source document or an export (an Excel via ClosedXML or a CSV via CsvHelper) the API hands back a SAS link valid for, say, fifteen minutes pointing at [[Azure Blob Storage]]. After it lapses the link is dead, so it's safe to email or put in a response. It's a capability-style alternative to routing every byte through the API, and it leans on the same expiry mindset as a [[Bearer Token]].

## Source
KBA AI Document Ingestion project

---

## Neighbors — *what lives nearby*
Both [[Bearer Token]] and SAS tokens are short-lived, scoped credentials embedded in a request. [[Authorization]] is encoded right into a SAS URL itself — the token specifies exactly "what you may do."

## Clash — *what pushes against this*
A [[Connection String]] sits at the opposite end of the spectrum: it's a full, long-lived account access that grants broad permissions, whereas a SAS token is a narrow, expiring grant.

## Roots — *where this comes from*
[[Azure Blob Storage]] uses SAS as the standard way to scope access to individual blobs. The bigger question underneath is [[Authentication]] — how do you grant access to a resource without sharing the master key?

## Paths — *where this leads*
SAS tokens enable secure, expiring document and export downloads from [[Azure Blob Storage]]. They also tie into [[Rate Limiting]] — issuing SAS links keeps heavy file transfers off the API itself instead of routing every byte through it.
