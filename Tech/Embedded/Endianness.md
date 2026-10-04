---
type: atomic
tags: [coding/embedded, coding/networking]
date: 2026-10-04
---

# Endianness

## Idea
A multi-byte number can be stored most-significant byte first (big-endian) or least-significant byte first (little-endian). It never matters until bytes cross from one system to another, and then it matters a lot.

## Definition
The 32-bit value `0x12345678` is laid out in memory as `12 34 56 78` on a **big-endian** machine and `78 56 34 12` on a **little-endian** one. x86 and most ARM configurations are little-endian; many older RISC chips and most network protocols are big-endian, which is why big-endian is also called **network byte order** and why C has `htons`/`htonl` and `ntohs`/`ntohl`. Inside one program you never notice, because the CPU reads its own format back consistently. Trouble starts when raw bytes leave: writing a struct straight to a file or socket, reading a sensor's register pair, parsing a binary protocol, or casting a byte buffer to an integer pointer. A two-byte temperature reading of `0x01 0x2C` means 300 if the sensor is big-endian and 11,265 if you read it the other way. The fix is to define the byte order in the format and convert explicitly at the boundary, assembling values with shifts rather than casts.

## Source
Danny Cohen coined "big-endian" and "little-endian" in "On Holy Wars and a Plea for Peace" (IEN 137, 1 April 1980; IEEE Computer, 1981), borrowing the terms from the egg-breaking factions in Swift's *Gulliver's Travels* (1726). Network byte order was fixed as big-endian in the early Internet RFCs.

---

## Compass

**Roots** — *where this comes from*
It comes from how the CPU lays out words in [[Memory-Mapped IO|memory]], and decoding byte-level layouts relies on the shifts and masks of [[Bit Manipulation]].

**Paths** — *where this leads*
Any binary protocol a [[Device Driver]] speaks has to state its byte order as part of the contract.

**Neighbors** — *what lives nearby*
Text formats like [[JSON]] sidestep the problem entirely by writing numbers as digits, at the cost of size and parsing speed compared with binary serialisation.

**Clash** — *what pushes against this*
Cohen's own point was that neither order is better; the real failure is not agreeing, which is why [[Define Contract Before Implementation]] matters more than which side you pick.
