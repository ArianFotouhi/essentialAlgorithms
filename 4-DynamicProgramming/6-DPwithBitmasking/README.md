### The Core Idea of Bitmask DP

In **Bitmask DP**, the state is a **subset of elements** represented as a binary mask.
Each bit (0 or 1) tells whether an element is included or not.

This lets us compactly encode **which elements have been visited/used**, and transitions are just **flipping bits** (add/remove an element).

This is the **subset analogue** of knapsack recursion — instead of moving to the next index, we move to the next **subset state**.

---

### What is Bitmask DP in More Technical Language?

Dynamic Programming with Bitmask = **recursively solving for subsets** and reusing them.

Formally:

* **State** = `(mask, extra_info)`

  * `mask`: bitmask of elements already chosen.
  * `extra_info`: usually the **last chosen element** (needed in TSP, matching, etc.).

* **Transition** = try adding an element not in the subset → set a new bit in the mask.

The recursion flows **over subsets**, building bigger subsets from smaller ones.

---

### When to Use Bitmask DP

* **Traveling Salesman / Hamiltonian Path**: visit all nodes with minimum cost.
* **Assignment Problems**: assign tasks to workers optimally.
* **Set Cover**: minimum cost to cover all requirements.
* **Counting Problems**: number of ways to build valid subsets/partitions.
* **Game States**: choosing from remaining elements.

---

### State & Transition (Mental Model)

**TSP Example:**

* **State:**
  `dp[mask][u] = minimum cost to visit all cities in mask, ending at u.`

* **Transition:**
  From `(mask, u)` → try adding a new city `v` not in `mask`:

  ```
  new_mask = mask | (1<<v)
  dp[new_mask][v] = min(dp[new_mask][v], dp[mask][u] + cost[u][v])
  ```

---

### General Pseudocode Idea

1. Define DP array for `(mask, last_element)`.
2. Loop over all subsets (`for mask in 0..(1<<n)-1`).
3. Inside, loop over possible last elements.
4. Try adding a new element (set a new bit).
5. Update DP for the new state.

---

### Quick Rules of Thumb

* `mask & (1<<i)` → check if `i` is in the subset.
* `mask | (1<<i)` → add `i` to the subset.
* `mask ^ (1<<i)` → remove `i` from the subset.
* Number of subsets = `2^n`. Works well for `n ≤ 20`.

---

### Complexity

* **Time:** `O(n * 2^n)` (most classic problems).
* **Space:** `O(n * 2^n)`.
* Works for `n ≈ 15–20` comfortably.

---

### Common Pitfalls

* Forgetting base cases (like `mask = 0` or `mask = full`).
* Confusing `|` (add) with `^` (remove).
* Not caching recursive calls → exponential time.
* Trying this when `n > 20` (too slow).

---

### Key Takeaways

* **Bitmask = subset state compression.**
* DP state is often `(mask, last)`.
* Build larger subsets from smaller ones.
* Perfect for **subset covering & assignment problems**.
* `O(n * 2^n)` → usually `n ≤ 20`.

