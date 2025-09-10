# Unbounded Knapsack — Infinite Item Supply

### The Core Idea

Unbounded Knapsack is just like 0/1 Knapsack — but **you can take each item as many times as you want**.
No restriction of “0 or 1” → it’s **0, 1, 2, 3… copies allowed**.

---

### Comparison with 0/1 Knapsack

| Aspect              | **0/1 Knapsack** (Pick/Not-Pick)        | **Unbounded Knapsack** (Complete)           |
| ------------------- | --------------------------------------- | ------------------------------------------- |
| Item usage          | At most **once** per item               | **Unlimited** copies per item               |
| Typical problems    | Subset sum, equal partition, Target Sum | Coin change, rod cutting, integer partition |
| Capacity loop order | **Backward** (to avoid reuse)           | **Forward** (to allow reuse)                |
| DP meaning          | Best/ways using **each item once**      | Best/ways using **items unlimited times**   |

---

### DP Transition (Key Difference)

**0/1 Knapsack:**

```python
for i in range(n):
    for w in range(W, wt[i]-1, -1):  # backward loop
        dp[w] = max(dp[w], dp[w - wt[i]] + val[i])
```

(backward loop prevents reusing item `i` multiple times in same iteration)

**Unbounded Knapsack:**

```python
for i in range(n):
    for w in range(wt[i], W+1):      # forward loop
        dp[w] = max(dp[w], dp[w - wt[i]] + val[i])
```

(forward loop **allows** reusing the same item — `dp[w - wt[i]]` already includes solutions that may use `i`)

---

### Real Examples

#### Coin Change (Count Ways)

Given coins `[1,2,5]`, count ways to make amount `11`:

```python
dp = [0]*(amount+1)
dp[0] = 1
for coin in coins:
    for x in range(coin, amount+1):  # forward loop
        dp[x] += dp[x - coin]
```

This counts combinations (order doesn’t matter).

#### Rod Cutting (Max Profit)

Given a rod of length `n` and price for each cut length:

```python
dp = [0]*(n+1)
for length in range(1, n+1):
    for L in range(length, n+1):  # forward loop = reuse allowed
        dp[L] = max(dp[L], price[length-1] + dp[L - length])
```

---

### When to Recognize "Use Unbounded Knapsack"

Think of it when you see:

* **Unlimited supply** / **infinite copies allowed**
* "You can take as many coins/items as you like"
* Problems asking for **combinations/ways** rather than just yes/no
* Problems like:

  * Coin Change (minimum coins, number of ways)
  * Rod Cutting (maximize revenue)
  * Integer partitions
  * Problems where you can repeat steps/items indefinitely

---

### Quick Mental Rule

* **Reverse loop ⇒ 0/1 knapsack (no reuse)**
* **Forward loop ⇒ unbounded knapsack (reuse allowed)**

