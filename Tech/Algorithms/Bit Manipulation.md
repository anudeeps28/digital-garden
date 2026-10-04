---
type: atomic
tags: [coding/algorithms, coding/embedded, learning]
date: 2026-10-04
---

# Bit Manipulation

## Idea
Treat an integer as a row of individual bits and use AND, OR, XOR and shifts to test, set or combine them, which makes some problems constant time and constant memory.

## Definition
A few identities do most of the work. `x & (x - 1)` clears the lowest set bit, so looping it until `x` is zero counts the 1 bits in as many steps as there are ones, and `x & (x - 1) == 0` tests for a power of two. `x & -x` isolates the lowest set bit. **XOR cancels pairs**: `a ^ a = 0` and `a ^ 0 = a`, so XOR-ing every number in an array where all values appear twice except one leaves that one; the **missing number** from 0..n falls out of XOR-ing all indices and values together. **Counting bits** for every number up to n reuses earlier answers: `bits[i] = bits[i >> 1] + (i & 1)`. **Sum without `+`** loops on `sum = a ^ b` (add without carry) and `carry = (a & b) << 1` until the carry is zero. Masks also pack many booleans into one integer: set with `|`, clear with `& ~`, toggle with `^`, test with `&`. In Python, integers are unbounded, so negative numbers need an explicit mask such as `0xFFFFFFFF`.

## Source
Peter Wegner published the `x & (x - 1)` counting trick in 1960 (Communications of the ACM); it is often called Kernighan's method because Brian Kernighan and Dennis Ritchie popularised it in *The C Programming Language* (1988 edition). MIT's HAKMEM memo (1972) and Henry S. Warren Jr.'s *Hacker's Delight* (2002) are the classic collections of bit tricks.

---

## Compass

**Roots** — *where this comes from*
Hardware is bits all the way down, and in embedded code a [[Memory-Mapped IO|memory-mapped register]] is configured by setting and clearing individual flag bits without disturbing the others.

**Paths** — *where this leads*
Bitmasks can represent subsets compactly, which lets [[Dynamic Programming]] index states by "which items are used so far", and bitsets make some [[Hash Table]] membership checks dramatically smaller.

**Neighbors** — *what lives nearby*
Byte order questions in [[Endianness]] sit right next to bit work, and permission flags like read, write and execute are bitmasks in the same style as [[Role-Based Access Control (RBAC)|role permissions]] stored compactly.

**Clash** — *what pushes against this*
Clever bit tricks are hard to read and easy to get wrong with signed numbers or language-specific integer widths, so outside hot paths a clear boolean beats a cryptic mask; the [[Big-O Notation]] gain is often a constant factor at best.
