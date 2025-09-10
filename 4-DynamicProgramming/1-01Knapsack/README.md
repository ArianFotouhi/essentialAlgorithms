# 0/1 Knapsack & Subset Sum — Pick/Not-Pick Decisions


### The Core Idea of 0/1 Knapsack

Imagine you are a thief with a bag (knapsack) that can hold up to `W` weight.
You have n items, each with:

`weight[i]`

`value[i]`

Your goal: maximize total value without exceeding `W`.

But you have a catch: for each item, you can either take `0` of it or `1` of it — no fractions, no multiple copies.
That’s why it’s called 0/1 Knapsack.

### What is 0/1 Knapsack in more techincal language?
A classic DP problem: given `n` items with `(weight, value)` and a capacity `W`, choose a subset of items (each at most once) to maximize value without exceeding capacity.

**Subset Sum:** special case where we only care whether some subset sums to exactly a target (boolean answer).

Both use the **pick / not-pick** pattern — at each item, you decide to include it (if possible) or skip it, and recurse.

---

### When to Use Pick/Not-Pick DP
- **Knapsack-like targets (capacity):** select items under capacity/weight/limit.
- **Subset selection problems:** find subset with target sum, equal partition, min difference.
- **Maximize / Minimize:** profit, score, or cost.
- **Count ways:** number of subsets reaching a sum.
- **Yes/No existence:** can we achieve this sum?

---

### State & Transition (Mental Model)
**State:**  
- `i` = index of current item  
- `w` = remaining capacity / remaining target sum  

**Transition:**  
- **Skip:** solve for `i+1, w`  
- **Take:** solve for `i+1, w - wt[i]` (only if `wt[i] <= w`)  

Take the **max / min / OR / sum** depending on the problem:
- Knapsack → max of values
- Subset sum existence → OR (boolean)
- Count subsets → sum counts from both branches

---

### Pick/Not-Pick Recursion Template

```python
from functools import lru_cache

@lru_cache(None)
def dfs(i, w):
    if i == n:                # base: no items left
        return 0              # or True/False/0 ways depending on problem
    res = dfs(i+1, w)         # not pick
    if wt[i] <= w:            # pick if fits
        res = max(res, val[i] + dfs(i+1, w - wt[i]))
    return res
````

---

### Bottom-Up Tabulation

```python
dp = [[0]*(W+1) for _ in range(n+1)]
for i in range(n-1, -1, -1):
    for w in range(W+1):
        dp[i][w] = dp[i+1][w]  # skip
        if wt[i] <= w:
            dp[i][w] = max(dp[i][w], val[i] + dp[i+1][w - wt[i]])
```

Space-optimized to **1D array** (reverse iterate `w`):

```python
dp = [0]*(W+1)
for i in range(n):
    for w in range(W, wt[i]-1, -1):
        dp[w] = max(dp[w], val[i] + dp[w - wt[i]])
```

---

### Quick Rules of Thumb

* **Reverse iteration** for 0/1 knapsack (ensures each item used ≤ once).
* **Forward iteration** for unbounded knapsack (allows reuse).
* Boolean DP uses `or` for existence, integer DP uses `+` for counts.
* Subset Sum is just knapsack with `val[i] = wt[i]` and target `W`.

---

### Complexity

* **Time:** `O(nW)` (n = items, W = capacity/target)
* **Space:** `O(nW)` → `O(W)` with 1D compression
* **Recursion depth:** O(n) for top-down

---

### Common Pitfalls

* Iterating forward for 0/1 knapsack → accidentally reuses item multiple times.
* Wrong base case: forgetting that making sum `0` is always possible (True).
* Forgetting to handle item weights > current capacity (should just skip).
* Using wrong combination logic: `max` vs. `+` vs. `or`.

---

### Practice Problems

* **0/1 Knapsack:** LeetCode 416 (Partition Equal Subset Sum), 494 (Target Sum)
* **Subset Sum:** classic interview problem, also 698 (Partition to k Equal Sum Subsets)
* **Count of Subsets:** LeetCode 494 (Target Sum)
* **Min Difference Partition:** subset sum variant minimizing |sum1 - sum2|

---

### Key Takeaways

* **Pick / Not-Pick = binary choice tree → DP.**
* **Post-order solve:** compute results of children (pick/skip) before combining.
* Use **reverse loops** for space optimization.
* Most subset/knapsack problems are just variations of this pattern.
* Memorization converts exponential recursion to polynomial time.

```


