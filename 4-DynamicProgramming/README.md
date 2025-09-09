# Dynamic Programming — Core Techniques

0/1 Knapsack • Subset Sum (Pick/Not-Pick) • Unbounded Knapsack • Coin Change • Rod Cutting • DP on Strings (LCS, Edit Distance, Palindromes) • DP on Subarrays • DP on Trees • Bitmask DP (TSP, subset states) • State Compression

---

## 📌 Mental Model

**DP = Optimal substructure + overlapping subproblems.**  
Define a **state** that captures “how far” you’ve solved, write a **transition** that picks the best among choices, initialize **base cases**, and choose **top-down (memo)** or **bottom-up (tabulation)**. Optimize space when only a few previous layers are needed.

- Ask:  
  1) What decisions are made at step *i*?  
  2) What parameters uniquely describe a subproblem?  
  3) Is the answer a **count**, **min/max**, or **boolean**?

**Patterns:**  
- 1D DP (prefix/length/amount)  
- 2D DP (i vs. j: indices, capacities, edit pointers)  
- Knapsack family (bounded/unbounded)  
- Subsequence vs. Subarray (non-contiguous vs. contiguous)  
- Partitioning (cut the array/string and combine)  
- Tree DP (post-order combine children)  
- Bitmask DP (subset states)

---

## When to Use What

- **0/1 Knapsack / Subset Sum:** choose each item ≤ once; capacity/target limits.
- **Unbounded Knapsack / Coin Change / Rod Cutting:** unlimited reuse of items; order may or may not matter.
- **Strings (LCS/Edit/Palindrome):** two pointers (i, j), compare chars; DP over prefixes.
- **Subarrays:** contiguous ranges; often Kadane or partition DP.
- **Trees:** compute from leaves up; post-order merges children info.
- **Bitmask / State Compression:** DP over subsets; n ≤ ~22–25 for full subsets.

---

## General Templates

### Top-Down (Memoization)

```python
from functools import lru_cache

@lru_cache(None)
def dp(args):
    # base cases
    # transitions
    return best
````

### Bottom-Up (Tabulation)

```python
# initialize dp with base states
for state in order:
    # transitions using earlier states
    dp[state] = combine(...)
```

**Space Optimization:** If `dp[i]` depends only on `dp[i-1]` (or same row), compress to 1D/rolling arrays and iterate indices carefully (reverse for 0/1 knapsack, forward for unbounded).

---

# 0/1 Knapsack & Subset Sum

## Problem Shape

* **0/1 Knapsack:** `n` items with `(wt[i], val[i])`, capacity `W`. Pick each item at most once to maximize value.
  **State:** `dp[i][w]` max value using items `0..i` with capacity `w`.
  **Transition:** take vs. skip `i`.

* **Subset Sum / Partition Equal:** check if a target sum is achievable with each element used at most once.
  **State:** `dp[w]` boolean: can we make sum `w`?

## Pick / Not-Pick Template (Top-Down)

```python
from functools import lru_cache

def knapsack_01(wt, val, W):
    n = len(wt)

    @lru_cache(None)
    def dfs(i, w):
        if i == n: return 0
        res = dfs(i+1, w)  # skip
        if wt[i] <= w:
            res = max(res, val[i] + dfs(i+1, w - wt[i]))  # take
        return res
    return dfs(0, W)
```

## 1D Boolean Subset Sum (Bottom-Up)

```python
def subset_sum(nums, target):
    dp = [False]*(target+1)
    dp[0] = True
    for x in nums:
        for s in range(target, x-1, -1):  # reverse for 0/1
            dp[s] = dp[s] or dp[s-x]
    return dp[target]
```

**Complexity:** `O(nW)` time, `O(W)` space (compressed).
**Gotchas:** reverse iteration for 0/1; forward would allow multi-use ⇒ wrong.

---

# Unbounded Knapsack Family

## Problem Shape

* **Unbounded Knapsack:** items can be picked unlimited times.
* **Coin Change (Count ways):** number of ways to form `amount` (order-independent).
* **Coin Change (Min coins):** min number of coins to form `amount`.
* **Rod Cutting:** rod length `N`, prices for lengths; cut into pieces for max profit.

## Unbounded Knapsack 1D (Max Value)

```python
def unbounded_knapsack(wt, val, W):
    dp = [0]*(W+1)
    for w in range(W+1):
        for i in range(len(wt)):
            if wt[i] <= w:
                dp[w] = max(dp[w], val[i] + dp[w - wt[i]])  # forward reuse
    return dp[W]
```

## Coin Change — Count Ways (Order-Independent)

```python
def coin_change_count(coins, amount):
    dp = [0]*(amount+1)
    dp[0] = 1
    for c in coins:                # outer: coins ⇒ combinations
        for a in range(c, amount+1):
            dp[a] += dp[a - c]
    return dp[amount]
```

## Coin Change — Min Coins

```python
def coin_change_min(coins, amount):
    INF = 10**9
    dp = [0] + [INF]* (amount)
    for a in range(1, amount+1):
        for c in coins:
            if c <= a:
                dp[a] = min(dp[a], 1 + dp[a - c])
    return dp[amount] if dp[amount] < INF else -1
```

## Rod Cutting (Equivalent to Unbounded)

```python
def rod_cutting(price):
    n = len(price)
    dp = [0]*(n+1)
    for L in range(1, n+1):
        for cut in range(1, L+1):
            dp[L] = max(dp[L], price[cut-1] + dp[L-cut])
    return dp[n]
```

**Gotchas:**

* For **count of permutations** (order matters), loop amount outermost then coins inner ⇒ counts sequences.

---

# DP on Strings

## Longest Common Subsequence (LCS)

```python
def lcs(A, B):
    n, m = len(A), len(B)
    dp = [[0]*(m+1) for _ in range(n+1)]
    for i in range(1, n+1):
        for j in range(1, m+1):
            if A[i-1] == B[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    return dp[n][m]
```

## Edit Distance (Levenshtein)

```python
def edit_distance(A, B):
    n, m = len(A), len(B)
    dp = [[0]*(m+1) for _ in range(n+1)]
    for i in range(n+1): dp[i][0] = i
    for j in range(m+1): dp[0][j] = j
    for i in range(1, n+1):
        for j in range(1, m+1):
            if A[i-1]==B[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(
                    dp[i-1][j-1],  # replace
                    dp[i-1][j],    # delete
                    dp[i][j-1]     # insert
                )
    return dp[n][m]
```

## Palindromes

**Longest Palindromic Subsequence (LPS):** LCS(A, reverse(A)).

**Min Cuts for Palindromic Partitioning:**

```python
def min_pal_cut(s):
    n = len(s)
    pal = [[False]*n for _ in range(n)]
    for i in range(n-1, -1, -1):
        for j in range(i, n):
            pal[i][j] = (s[i]==s[j]) and (j-i<=2 or pal[i+1][j-1])
    cuts = [0]*n
    for j in range(n):
        if pal[0][j]:
            cuts[j] = 0
        else:
            cuts[j] = min(cuts[i-1]+1 for i in range(1, j+1) if pal[i][j])
    return cuts[-1]
```

---

# DP on Subarrays

## Maximum Subarray Sum (Kadane)

```python
def kadane(nums):
    best = cur = nums[0]
    for x in nums[1:]:
        cur = max(x, cur + x)
        best = max(best, cur)
    return best
```

## Range/Partition DP (Cutting into Pieces)

Typical **partition DP** over intervals:
**State:** `dp[l][r]` = best for subarray `A[l..r]`.
**Transition:** try all split points `k` in `(l..r)`, combine left & right plus cost of merging/cut.

---

# DP on Trees (Post-Order)

## Example: Tree Diameter

```python
from collections import defaultdict
def diameter(n, edges):
    g = defaultdict(list)
    for u,v in edges:
        g[u].append(v); g[v].append(u)
    ans = 0
    def dfs(u, p):
        nonlocal ans
        best1 = best2 = 0
        for v in g[u]:
            if v==p: continue
            h = dfs(v, u) + 1
            if h>best1: best1,best2=h,best1
            elif h>best2: best2=h
        ans = max(ans, best1+best2)
        return best1
    dfs(0,-1)
    return ans
```

## Example: Max Independent Set on Tree

```python
def max_independent_set(n, edges, val):
    g = [[] for _ in range(n)]
    for u,v in edges: g[u].append(v); g[v].append(u)

    def dfs(u, p):
        take = val[u]
        skip = 0
        for v in g[u]:
            if v==p: continue
            t,s = dfs(v, u)
            take += s        # if take u, must skip v
            skip += max(t,s) # else choose best child
        return take, skip
    return max(dfs(0,-1))
```

---

# DP with Bitmasking

## Traveling Salesman (TSP, Held–Karp)

```python
def tsp(dist):
    n = len(dist)
    INF = 10**9
    dp = [[INF]*n for _ in range(1<<n)]
    dp[1][0] = 0
    for mask in range(1<<n):
        for i in range(n):
            if not (mask>>i)&1: continue
            if dp[mask][i] >= INF: continue
            for j in range(n):
                if (mask>>j)&1: continue
                nm = mask | (1<<j)
                dp[nm][j] = min(dp[nm][j], dp[mask][i] + dist[i][j])
    ans = min(dp[(1<<n)-1][i] + dist[i][0] for i in range(n))
    return ans
```

## Submask Iteration

```python
sub = mask
while True:
    # use sub
    if sub == 0: break
    sub = (sub-1) & mask
```

---

# State Compression

**Idea:** Encode multi-dimensional booleans/choices into a bitmask to reduce memory / speed transitions.

* **Grid DP with obstacles/tilings:** encode row frontier as a mask (profile DP).
* **Subset DP:** encode set of done tasks as `mask`.
* **Meet-in-the-Middle:** split set into halves, compute masks per half, combine (e.g., subset sum up to `n~40`).

---

## Complexity Cheats

* 0/1 Knapsack / Subset Sum: `O(nW)` time, `O(W)` space.
* Unbounded Knapsack / Coin Change: `O(nW)` or `O(amount * n)`.
* LCS/DP on two strings: `O(nm)` time, `O(min(n,m))` space (rolling).
* Edit Distance: `O(nm)` time, `O(min(n,m))` space possible.
* Palindromic substring DP: `O(n²)` time, `O(n²)` space.
* Interval DP: typically `O(n³)` (length × split).
* Tree DP: `O(n)` for many classic problems.
* Bitmask DP: `O(n·2^n)` to `O(n²·2^n)`.
* SOS DP: `O(n·2^n)`.

---

## Quick Reference Snippets

**Pick/Not-Pick (generic):**

```python
@lru_cache(None)
def solve(i, state):
    if i == n: return base
    ans = solve(i+1, state)               # not pick
    ans = combine(ans, pick(i, state))    # pick (if valid)
    return ans
```

**1D Knapsack Update Rules:**

```python
# 0/1 Knapsack
for w in range(W, wt-1, -1):
    dp[w] = max(dp[w], val + dp[w-wt])

# Unbounded Knapsack
for w in range(wt, W+1):
    dp[w] = max(dp[w], val + dp[w-wt])
```

**Submask Iteration:**

```python
sub = mask
while True:
    # use sub (includes 0 at end if needed)
    if sub == 0: break
    sub = (sub-1) & mask
```

