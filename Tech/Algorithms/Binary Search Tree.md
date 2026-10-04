---
type: atomic
tags: [coding/algorithms, coding/database, learning]
date: 2026-10-04
---

# Binary Search Tree

## Idea
A binary search tree keeps every smaller key in the left subtree and every larger key in the right, so you can search, insert and walk keys in order by following one path down.

## Definition
Each node has at most two children, and the **BST property** holds at every node: left subtree < node < right subtree. Search compares and goes left or right, taking O(h) where `h` is the height. A balanced tree has h ≈ log n; inserting sorted data into a naive BST builds a straight line with h = n, which is why **self-balancing** variants (AVL, red-black) exist. There are four standard **traversals**: pre-order (node, left, right), in-order (left, node, right), post-order (left, right, node), and level-order (breadth-first, row by row). **In-order traversal of a BST visits keys in sorted order**, which is the trick behind many problems: kth smallest element is the kth node of an in-order walk, and validating a BST means checking the in-order sequence is strictly increasing. **Lowest common ancestor** in a BST is the first node where the two targets split to different sides.

## Source
The binary search tree was discovered independently around 1960 by P. F. Windley, Andrew Donald Booth, Andrew Colin and Thomas N. Hibbard. Georgy Adelson-Velsky and Evgenii Landis published the first self-balancing version (AVL tree) in 1962, and Rudolf Bayer and Edward McCreight introduced the B-tree in 1970 (published 1972).

---

## Compass

**Roots** — *where this comes from*
It is [[Binary Search]] turned into a structure that stays searchable while you insert and delete, and its operations are naturally written with [[Recursion]].

**Paths** — *where this leads*
Database indexes use B-trees, a wide, shallow cousin designed for disk pages, which is why a lookup by [[Primary Key]] in a [[Relational Database]] takes a few page reads rather than a table scan.

**Neighbors** — *what lives nearby*
Its traversals are [[Breadth-First and Depth-First Search]] on a tree, and a [[Heap and Priority Queue|heap]] is a tree with a weaker ordering that only guarantees the minimum.

**Clash** — *what pushes against this*
For pure key lookups a [[Hash Table]] is faster on average, and an unbalanced BST quietly degrades to a [[Linked List]] with O(n) operations.
