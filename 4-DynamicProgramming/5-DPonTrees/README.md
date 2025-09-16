### The Core Idea of Tree DP

In **Tree DP**, each node’s answer depends on the answers of its children.
You traverse the tree in **post-order** (children first, then parent) to ensure all child-subproblems are solved before combining them at the parent.

This is the tree analogue of **pick / not-pick recursion** in knapsack — but instead of binary choices, you combine **subtree contributions**.

---

### What is Tree DP in More Technical Language?

Dynamic Programming on Trees = **recursively computing values for subtrees** and reusing them.

Formally:

* **State** = a node (sometimes with extra parameters like “is parent taken/colored?”).
* **Transition** = combine DP results from all children.

The recursion always flows **upward** (post-order), since parent needs children’s answers.

---

### When to Use Post-Order Tree DP

* **Subtree properties:** size, height, sum of values, number of paths.
* **Parent depends on children:** maximum independent set, vertex cover, coloring, DP with constraints.
* **Path or subtree optimization:** longest path, diameter, max/min cost from root to leaves.
* **Counting problems:** number of valid colorings, number of ways to select nodes.

---

### State & Transition (Mental Model)

**State Example 1 (Subtree DP):**
`dp[u] = best answer for subtree rooted at u`.

**State Example 2 (With Choices):**

* `dp[u][0] = best if u not taken`
* `dp[u][1] = best if u taken`

**Transition:**

* Traverse children.
* Combine their dp answers into parent’s dp.

---

### Post-Order Recursion Template

```python
from functools import lru_cache
import sys
sys.setrecursionlimit(10**6)

def dfs(u, parent):
    # base init (e.g. subtree_size = 1 for itself)
    res = base_value
    
    for v in tree[u]:
        if v == parent: continue
        child = dfs(v, u)        # solve child first (post-order)
        res = combine(res, child) # merge child contribution
    
    dp[u] = res
    return dp[u]
```

---

### Example 1: Subtree Size

```python
def dfs(u, parent):
    size = 1
    for v in tree[u]:
        if v == parent: continue
        size += dfs(v, u)
    dp[u] = size
    return dp[u]
```

---

### Example 2: Maximum Independent Set (Tree Version of Pick/Not-Pick)

```python
def dfs(u, parent):
    take = val[u]
    skip = 0
    for v in tree[u]:
        if v == parent: continue
        child_take, child_skip = dfs(v, u)
        take += child_skip       # if we take u, children can’t be taken
        skip += max(child_take, child_skip)  # else children are free
    
    return take, skip
```

Answer = `max(dfs(root))`.

---

### Bottom-Up Tabulation on Trees

Unlike arrays, we usually can’t tabulate trees easily because there’s no natural linear order.
Instead, **DFS recursion = implicit post-order tabulation**.

Sometimes, for **rerooting DP**, we do an extra top-down pass after the post-order bottom-up pass.

---

### Quick Rules of Thumb

* Always solve **children first → parent next** (post-order).
* Use tuples `(take, skip)` or arrays `dp[u][state]` if multiple states exist.
* For **path problems**, track both “best in subtree” and “best through node”.
* For **rerooting problems** (like max sum if root moves), you often need **two DFS passes**.

---

### Complexity

* **Time:** `O(n)` (each edge visited once).
* **Space:** `O(n)` for recursion + dp storage.
* **Recursion depth:** O(n) worst-case (avoid with sys.setrecursionlimit or iterative).

---

### Common Pitfalls

* Forgetting to skip the parent during DFS → infinite recursion.
* Double counting contributions (always carefully define what `dp[u]` represents).
* Mixing up **global best** (like diameter) with **subtree best** (local dp).
* Not separating **taken vs not-taken states** in problems like independent set.

---

### Practice Problems

* **Subtree Size:** Count nodes in each subtree.
* **Tree Height / Diameter:** Longest path in tree.
* **Maximum Independent Set on Trees** (classic).
* **Vertex Cover on Trees.**
* **Tree DP + Rerooting:** sum of distances from each node to all others.

---

### Key Takeaways

* **Post-order = child first, parent after → perfect for subtree DP.**
* States often = `dp[node][something]`.
* Tree DP = knapsack-style DP, but branching depends on children instead of next index.
* Rerooting = two DFS passes (post-order bottom-up + top-down adjust).

