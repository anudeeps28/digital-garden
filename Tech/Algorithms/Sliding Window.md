---
type: atomic
tags: [coding/algorithms, learning]
date: 2026-10-04
---

# Sliding Window

## Idea
Keep a running summary of a contiguous range and slide that range forward, adding what enters on the right and removing what leaves on the left, instead of recomputing every subarray from scratch.

## Definition
A **fixed window** has constant width: the sum of every 7-day block is one addition and one subtraction per step. A **variable window** grows its right edge every step and shrinks its left edge only while a rule is broken. Longest substring without repeating characters is the canonical case: extend right, and when a character repeats, move left past its previous position, tracking the best length seen. Longest repeating character replacement keeps a window valid while `window length − count of most frequent char ≤ k`. Best time to buy and sell a stock is a window whose left edge jumps to any new minimum price. The state inside the window is usually a counter, a set, or a [[Hash Table]] of frequencies. Because each element enters and leaves at most once, the whole scan is O(n).

## Source
No single inventor; the algorithmic pattern grew out of array-processing folklore and is now standard interview vocabulary. The name echoes the sliding window protocol in networking, used for flow control in TCP (Cerf and Kahn, 1974), where the "window" is the range of bytes a sender may have in flight.

---

## Compass

**Roots** — *where this comes from*
It is the same-direction form of the [[Two-Pointer Technique]], and it exists to bring brute-force O(n²) or worse down to linear in [[Big-O Notation]] terms.

**Paths** — *where this leads*
The identical shape appears in production as [[Rate Limiting]], where a sliding window counts requests in the last N seconds and evicts timestamps that fall out of range.

**Neighbors** — *what lives nearby*
Kadane's maximum subarray in [[Dynamic Programming]] is a near cousin that decides at each step whether to extend or restart, and sliding window maximum is solved with a monotonic deque from [[Stack and Queue]].

**Clash** — *what pushes against this*
The variable window only works when shrinking the window can restore validity, which fails if the array has negative numbers for sum constraints; then you need prefix sums or a different approach.
