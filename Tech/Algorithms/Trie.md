---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Trie

## Idea
A trie stores strings character by character along the branches of a tree, so every word with the same prefix shares the same path and prefix lookups are fast.

## Definition
Each node holds a map from character to child node plus a flag marking "a word ends here". Inserting or searching a word of length `L` walks `L` nodes, independent of how many words are stored, and `startsWith(prefix)` is the same walk without checking the end flag. That makes tries the natural structure for autocomplete, spell checking and IP routing tables (longest-prefix match). A word dictionary that supports wildcards, where `.` matches any letter, switches to a depth-first search that branches into every child at a wildcard. Word Search II combines a trie with grid backtracking: load all target words into a trie, then DFS from each cell and abandon a path the moment its prefix is not in the trie, pruning far more than checking each word separately. Memory is the cost; **compressed tries** (radix or Patricia trees) merge single-child chains to save space.

## Source
René de la Briandais described the structure in 1959, and Edward Fredkin named it "trie", from the middle of "retrieval", in 1960. Donald R. Morrison's PATRICIA (1968) introduced the compressed form.

---

## Compass

**Roots** — *where this comes from*
It is a tree searched with [[Breadth-First and Depth-First Search]], and its child maps are often small [[Hash Table|hash tables]] or fixed arrays of 26 slots.

**Paths** — *where this leads*
Search engines start from the same need, and an inverted index scored with [[BM25 Scoring]] is the text-retrieval answer once you need relevance rather than exact prefixes.

**Neighbors** — *what lives nearby*
A [[Binary Search Tree]] also keeps keys in order, but compares whole keys at each node, while a trie compares one character at a time. Radix sort in [[Sorting Algorithms]] processes keys digit by digit in the same spirit.

**Clash** — *what pushes against this*
Tries find exact and prefix matches only. Finding text by meaning needs [[Vector Search]], and for plain membership checks a hash set uses far less memory.
