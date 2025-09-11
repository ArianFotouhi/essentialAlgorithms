# DP on Strings — Core Patterns

## The Core Idea
Dynamic Programming on strings breaks a string (or two strings) into **prefixes/substrings** and builds the solution from smaller subproblems.  
You usually define `dp[i][j]` to represent something about the first `i` characters of one string and the first `j` characters of another (or about substring `s[i..j]` of a single string).

**Key Insight:**  
Many string problems are about **comparing prefixes**, **matching characters**, or **making choices** based on current character(s) and previously solved results.

---

## Typical String DP Problems

| Problem Type | What `dp[i][j]` Means | Typical Use |
|-------------|----------------------|-------------|
| **LCS** (Longest Common Subsequence) | length of LCS of `s1[0..i-1]` & `s2[0..j-1]` | Find longest subsequence common to both strings |
| **Edit Distance** | min operations to convert `s1[0..i-1]` → `s2[0..j-1]` | Spell check, string similarity |
| **Palindrome DP** | `True/False` if `s[i..j]` is palindrome OR length of LPS in `s[i..j]` | Longest palindrome, minimum insertions to make palindrome |

---

## DP Transition (Key Idea)

### 1. LCS (Longest Common Subsequence)

```python
for i in range(1, n+1):
    for j in range(1, m+1):
        if A[i-1] == B[j-1]:
            dp[i][j] = 1 + dp[i-1][j-1]
        else:
            dp[i][j] = max(dp[i-1][j], dp[i][j-1])
```

**When characters match → take diagonal +1** Otherwise take the **best of left/up**.


### 2. Edit Distance (Levenshtein)

```python
for i in range(1, n+1):
    for j in range(1, m+1):
        if A[i-1] == B[j-1]:
            dp[i][j] = dp[i-1][j-1]
        else:
            dp[i][j] = 1 + min(
                dp[i-1][j],   # delete
                dp[i][j-1],   # insert
                dp[i-1][j-1]  # replace
            )
```

**When characters match → carry diagonal**
Otherwise take **1 + min(delete, insert, replace)**.

---

### 3. Palindrome Problems

#### Longest Palindromic Subsequence (LPS)

```python
for length in range(2, n+1):
    for i in range(0, n-length+1):
        j = i + length - 1
        if s[i] == s[j]:
            dp[i][j] = 2 + dp[i+1][j-1]
        else:
            dp[i][j] = max(dp[i+1][j], dp[i][j-1])
```

Diagonal-based, like LCS but on a single string.

---

#### Longest Palindromic Substring

```python
for i in range(n):
    dp[i][i] = True  # single chars are palindrome
for i in range(n-1):
    dp[i][i+1] = (s[i] == s[i+1])
for length in range(3, n+1):
    for i in range(0, n-length+1):
        j = i+length-1
        dp[i][j] = (s[i] == s[j]) and dp[i+1][j-1]
```

---

## When to Recognize "Use DP on Strings"

Think of DP when you see:

* **Two strings** being compared character by character
* **Min/max count** of operations to transform strings
* **"Longest subsequence/substring"** type questions
* **Palindrome-related** questions (LPS, min insertions/deletions)
* **Overlapping subproblems** — brute force recursion would repeat work

---

## Real Examples

* **LCS:** Find similarity of DNA sequences, version control diff
* **Edit Distance:** Autocorrect suggestions (`kitten → sitting`)
* **Palindrome DP:**

  * Longest Palindromic Subsequence (`bbbab → bbbb`)
  * Minimum insertions to make string palindrome

---

## Quick Mental Rules

* **Two strings?** → probably `dp[i][j]` over prefixes
* **Matching chars?** → diagonal relation (`i-1, j-1`)
* **Operations allowed (insert/delete/replace)?** → edit distance
* **Palindrome?** → think symmetry, reverse, or `dp[i][j]` over substring
* **Subsequence vs Substring:**

  * Subsequence → look at LCS-style DP
  * Substring → look at contiguous range DP or center expansion

