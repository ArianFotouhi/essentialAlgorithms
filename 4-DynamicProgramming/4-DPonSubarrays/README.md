# DP on Subarrays — Max Subarray Sum & Palindromic Partitions

## The Core Idea

“DP on subarrays” means your state depends on a contiguous slice `s[l..r]`.
Two classic patterns:

1. **Kadane-style** (prefix-to-index): build best answer ending at index `i`.
2. **Interval DP (length-based)**: build answers for all intervals `[l, r]`, usually by increasing length.

---

## Comparison at a Glance

| Aspect           | Kadane-style (prefix DP)                                      | Interval DP (length DP)                                                                     |
| ---------------- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Typical problems | Max subarray sum, max product subarray, max circular subarray | Palindromic partitions (min cuts), count pal substrings, matrix chain mult., burst balloons |
| State meaning    | `best_ending_at[i]`, sometimes also `best_so_far`             | `dp[l][r]` describes the optimal/feasible result on `s[l..r]`                               |
| Build order      | Left → right (single pass)                                    | By subarray length `len = 1..n` (nested loops over `l, r`)                                  |
| Transition shape | Extend vs restart at `i`                                      | Split at a `k` or shrink ends; often uses helper `isPal[l][r]`                              |
| Time & space     | O(n) time, O(1) or O(n) space                                 | O(n²) time/space (common), sometimes O(n³) if naïve splits                                  |

---

## Part A: Max Subarray Sum (Kadane)

### DP Meaning

* `best_end[i]`: max sum of a subarray that **must end** at `i`.
* `ans`: max over all `best_end[i]`.

### Transition (Key)

```
best_end[i] = max(nums[i], best_end[i-1] + nums[i])  # extend or restart
ans = max(ans, best_end[i])
```

### Code (O(n) / O(1))

```python
def max_subarray(nums):
    best_end = ans = nums[0]
    for x in nums[1:]:
        best_end = max(x, best_end + x)
        ans = max(ans, best_end)
    return ans
```

#### Variants (quick drops)

* **Also return indices**: track start when you “restart”.
* **Max circular subarray**: `max(Kadane(nums), total_sum - min_subarray_sum)`; handle all-negative case.
* **Max product subarray**: track `max_end` and `min_end` because negatives flip roles.

---

## Part B: Palindromic Partitions (Interval DP)

### Two common tasks

1. **Min cuts** to partition `s` into palindromes.
2. **Count palindromic substrings** (or list them).

They share a helper: **palindrome table** `isPal[l][r]`.

### Precompute Palindrome Table

`isPal[l][r] = True` iff `s[l] == s[r]` and (length ≤ 2 or `isPal[l+1][r-1]`).

```python
def build_is_pal(s):
    n = len(s)
    isPal = [[False]*n for _ in range(n)]
    for i in range(n): isPal[i][i] = True
    for l in range(n-1, -1, -1):
        for r in range(l+1, n):
            if s[l] == s[r] and (r-l == 1 or isPal[l+1][r-1]):
                isPal[l][r] = True
    return isPal
```

### Min Cuts for Palindromic Partition

#### DP Meaning

* `cut[i]`: min cuts needed for prefix `s[:i+1]`.

#### Transition

* If `s[0..i]` pal ⇒ `cut[i] = 0`.
* Else `cut[i] = 1 + min(cut[j] for j < i if s[j+1..i] pal)`.

```python
def min_cut_pal(s):
    n = len(s)
    isPal = build_is_pal(s)
    cut = [0]*n
    for i in range(n):
        if isPal[0][i]:
            cut[i] = 0
        else:
            best = i  # worst: cut between every char
            for j in range(i):
                if isPal[j+1][i]:
                    best = min(best, cut[j] + 1)
            cut[i] = best
    return cut[-1]
```

### Count All Palindromic Substrings

Two ways:

**(1) Expand Around Center (O(n²), O(1))**

```python
def count_pal_substrings(s):
    n, ans = len(s), 0
    def expand(L, R):
        nonlocal ans
        while L >= 0 and R < n and s[L] == s[R]:
            ans += 1
            L -= 1; R += 1
    for c in range(n):
        expand(c, c)     # odd length
        expand(c, c+1)   # even length
    return ans
```

**(2) Using `isPal` table:** sum `isPal[l][r]` over all pairs (same complexity, more memory).

---

## Real Examples

### 1) Max Subarray Sum (standard)

Input: `[-2,1,-3,4,-1,2,1,-5,4]`
Answer: `6` (from `[4,-1,2,1]`).

### 2) Max Circular Subarray

Compute:

* `best_normal = Kadane(nums)`
* `best_wrap = total - min_subarray_sum`
* Handle all-negative (`best_wrap == 0` ⇒ use `best_normal`).

### 3) Palindromic Partition (min cuts)

`s = "aab"` → partitions: `"aa" | "b"` → min cuts = `1`.

### 4) Count Palindromic Substrings

`s = "aaa"` → substrings: `"a","a","a","aa","aa","aaa"` → count `6`.

---

## When to Use Which

Think **Kadane** when you see:

* “maximum sum/product **subarray**”
* “best subarray ending at i” choices of **extend vs restart**
* One pass left→right makes sense

Think **Interval DP** when you see:

* Subproblems on **`[l..r]`** slices
* Need to **split** or **shrink ends**
* Palindrome checks, matrix-chain-like splits, min-cuts, counting substrings

---

## Loop Orders (Quick Mental Rule)

* **Kadane-style**: single forward pass over indices.
* **Interval DP**:

  * If using `isPal`: fill table with `l` decreasing, `r` increasing (or by length).
  * For `dp[l][r]` with splits: loop `len = 1..n`, then `l`, then split point `k`.

---

## Patterns You’ll Reuse

* **Restart-or-Extend template** (max-sum, max-product, longest positive subarray):

  ```
  dp[i] = combine(current, extend(dp[i-1], current))
  ans = best(ans, dp[i])
  ```

* **Length-based interval template**:

  ```
  for len in 1..n:
      for l in 0..n-len:
          r = l+len-1
          dp[l][r] = min/max over:
              shrink-ends or split at k
  ```

* **Palindrome helper**: precompute `isPal` once; reuse for min-cuts, counting, enumerating partitions.

---

## Quick Cheatsheet

* “Extend vs restart” → **Kadane** (O(n))
* “Split / `[l..r]` intervals\`” → **Interval DP** (O(n²))
* Precompute `isPal` to make palindrome questions fast
* Circular max subarray → **Kadane + min-subarray trick**
* Counting pal substrings fast → **expand around center**

