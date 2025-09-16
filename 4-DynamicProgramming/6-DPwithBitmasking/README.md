### The Core Idea of DP with Bitmasking

In **Bitmask DP**, the state represents a **subset of elements** using a bitmask.
Each bit (0/1) in the mask encodes whether an element is included.

This allows us to represent subsets compactly and transition between them by **adding/removing one element at a time**.

This is the subset analogue of **pick / not-pick recursion** in knapsack — but instead of a binary branch, we keep track of **which subset we are currently in**.

---

### What is Bitmask DP in More Technical Language?

Dynamic Programming with Bitmask = **recursively computing answers for subsets** and reusing them.

Formally:

* **State** = `(mask, extra_info)` where

  * `mask` is a bitmask representing the set of visited/used elements.
  * `extra_info` is often the **last element chosen** (important in problems like TSP).

* **Transition** = try adding a new element (set a bit in the mask) or removing one (clear a bit).

The recursion flows **over subsets** — each new state builds on smaller subsets.

---

### When to Use Bitmask DP

* **Subset problems:** Traveling Salesman, Hamiltonian paths, Steiner trees.
* **Covering problems:** set cover, minimum cost to cover requirements.
* **Counting problems:** number of valid subsets, number of ways to partition.
* **Assignment problems:** matching tasks to workers, minimum cost bipartite matching.
* **Game DP:** states where players can choose from remaining elements.

---

### State & Transition (Mental Model)

**State Example 1 (TSP):**

```text
dp[mask][u] = min cost to visit all nodes in `mask`, ending at `u`.
```

**Transition:**

```text
dp[mask][u] = min( dp[mask ^ (1<<u)][v] + cost[v][u] )
              for all v in mask, v != u
```

---

### Subset Recursion Template

```python
from functools import lru_cache

@lru_cache(None)
def dp(mask, u):
    if mask == (1 << n) - 1:  # all visited
        return cost[u][0]     # return to start
    
    ans = float('inf')
    for v in range(n):
        if not (mask & (1 << v)):  # if v not visited
            ans = min(ans, cost[u][v] + dp(mask | (1 << v), v))
    
    return ans

# Start: only city 0 visited, currently at city 0
answer = dp(1, 0)
```

---

### Example 1: Traveling Salesman Problem (TSP)

* **State:** `(mask, u)` = visited set `mask`, ending at city `u`.
* **Transition:** add one more unvisited city `v`.
* **Base case:** all cities visited → return cost to start.

Time Complexity: `O(n * 2^n)`.

---

### Example 2: Counting Subsets with Constraints

```python
@lru_cache(None)
def count(mask):
    if mask == 0: return 1  # empty set
    
    ans = 0
    for v in range(n):
        if mask & (1 << v):   # if v is in subset
            ans += count(mask ^ (1 << v))  # remove v
    
    return ans
```

This counts **all subsets** recursively.

---

### Bottom-Up Tabulation for Bitmask DP

Instead of recursion, iterate over all masks:

```python
dp = [[inf] * n for _ in range(1 << n)]
dp[1][0] = 0   # start from city 0

for mask in range(1 << n):
    for u in range(n):
        if not (mask & (1 << u)): continue
        for v in range(n):
            if mask & (1 << v): continue
            new_mask = mask | (1 << v)
            dp[new_mask][v] = min(dp[new_mask][v], dp[mask][u] + cost[u][v])
```

---

### Quick Rules of Thumb

* Use `mask & (1<<i)` to check if `i` is in the subset.
* Use `mask | (1<<i)` to add `i` to the subset.
* Use `mask ^ (1<<i)` to remove `i` from the subset.
* Iterating over subsets = loop `mask in range(1<<n)`.
* Number of subsets = `2^n` → works up to `n ≈ 20`.

---

### Complexity

* **Time:** `O(n * 2^n)` (typical for TSP/assignment problems).
* **Space:** `O(n * 2^n)` for DP table.
* Works well up to `n = 20` (≈ 20 million states).

---

### Common Pitfalls

* Forgetting to include the base case (`mask == full` or `mask == 0`).
* Mixing up `mask | (1<<v)` and `mask ^ (1<<v)`.
* Not memoizing recursion → exponential blowup.
* Large `n` (e.g., `n=25`) → `O(25 * 2^25)` is too big.

---

### Practice Problems

* Traveling Salesman Problem (classic).
* Assignment problem (minimum cost bipartite matching).
* Counting Hamiltonian paths.
* Set cover with minimum cost.
* Subset DP for counting partitions.

---

### Key Takeaways

* **Bitmask = subset state compression.**
* State is usually `(mask, last)` or `(mask, extra_info)`.
* Transitions = add/remove elements (bit operations).
* Perfect for **TSP-style covering problems** and **assignment problems**.
* `n ≤ 20` is the sweet spot.

