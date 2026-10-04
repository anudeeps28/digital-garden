---
type: atomic
tags: [coding/algorithms, coding/database, learning]
date: 2026-10-04
---

# Hash Table

## Idea
A hash table turns a key into an array index with a hash function, so inserts and lookups take constant time on average no matter how much data you store.

## Definition
A **hash function** maps a key to a bucket number; the table stores the value in that bucket. Two keys landing in the same bucket is a **collision**, and there are two main ways to handle it. **Chaining** keeps a small list in each bucket and appends colliding entries. **Open addressing** stores everything in the array itself and, on a collision, probes for another slot: **linear probing** tries the next slot, **quadratic probing** jumps by 1, 4, 9 and so on to avoid clusters. Performance depends on the **load factor** (entries divided by buckets); when it gets too high, the table resizes and rehashes. Two Sum is the classic use: walk the array once, and for each number check whether `target − number` is already in the table. Group Anagrams shows a smarter key: sort each word's letters (or count them) so all anagrams hash to the same bucket. Python's `dict` and `set`, and C++'s `unordered_map`, are hash tables.

## Source
Hans Peter Luhn described hashing with chaining in an internal IBM memo in January 1953. Around the same time, Gene Amdahl, Elaine McGraw, Nathaniel Rochester and Arthur Samuel at IBM used open addressing with linear probing (credited to Amdahl; Andrey Ershov had the same idea independently). Arnold Dumey published the first open description in 1956, and Robert Morris put the word "hashing" into print in 1968.

---

## Compass

**Roots** — *where this comes from*
It is the tool that most often turns an O(n²) search into O(n) in [[Big-O Notation]], and it is the default data structure behind any keyed lookup.

**Paths** — *where this leads*
[[In-Memory Caching]] is a hash table with eviction rules, and the memo in [[Dynamic Programming]] is usually one too. Databases use hash indexes for exact-match lookups on a [[Primary Key]].

**Neighbors** — *what lives nearby*
The frequency counter inside a [[Sliding Window]] is a small hash table, and [[Union-Find]] often uses one to map arbitrary labels to set ids.

**Clash** — *what pushes against this*
Hashing destroys order, so range queries and "next larger key" need a [[Binary Search Tree]] or sorted array instead; a [[Trie]] beats it for prefix queries. Worst-case lookups degrade to O(n) when many keys collide, which attackers can exploit with crafted inputs.
