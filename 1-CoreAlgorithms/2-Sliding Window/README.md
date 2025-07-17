# 🚪 Sliding Window Technique – Explained

The **Sliding Window** technique is a powerful and efficient pattern used to solve problems involving **contiguous sequences** in arrays or strings. It's especially useful when optimizing **subarray or substring problems** that involve sum, length, or frequency of elements.

---

## 📌 What Is Sliding Window?

Sliding Window is a technique where a "window" (a subrange of elements) **moves across the data structure** to inspect or maintain a subset of values **without reprocessing the entire structure each time**.

Instead of using nested loops to examine each subarray or substring (which is expensive), you "slide" a fixed or variable-sized window to achieve linear time complexity.

---

## ⚡ Why Use Sliding Window?

- Significantly reduces time complexity from **O(n²)** to **O(n)**.
- Allows solving many problems **in-place**, without extra memory.
- Makes it easy to maintain running statistics like:
  - Sum
  - Frequency
  - Distinct element count
  - Max/min values

---

## 🎯 When to Use Sliding Window?

Think about using Sliding Window when:

- The problem involves **contiguous subarrays or substrings**.
- You need to:
  - **Find the longest or shortest** window meeting a condition.
  - **Maintain a count** or **sum** of items in a range.
  - Track **frequency**, **uniqueness**, or **distinct elements**.
- You're told to work with a **window size**, or optimize over a **range**.

---

## 🔧 Types of Sliding Windows

| Type                  | Description                            | Example Use Case                                 |
|-----------------------|----------------------------------------|--------------------------------------------------|
| **Fixed-size window** | Window size `k` remains constant       | Maximum sum of subarray of size k                |
| **Dynamic window**    | Window grows or shrinks as needed      | Longest substring without repeating characters   |
| **Shrinking window**  | Window is adjusted based on constraint | Substring with at most k distinct characters     |

---

## 🧠 Core Idea

1. **Expand** the window by moving the right pointer.
2. **Shrink** the window by moving the left pointer (when constraint is violated).
3. Update result **dynamically** (length, count, sum, etc.)

---

## 🧪 Common Problems to Practice

| Problem | Type |
|--------|------|
| [Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/) | Fixed-size |
| [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | Dynamic |
| [Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) | Shrinking |
| [Permutation in String](https://leetcode.com/problems/permutation-in-string/) | Fixed-size + Frequency |
| [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) | Shrinking + Frequency |

---

## 📘 Summary

- The **Sliding Window** pattern is critical for solving efficient substring/subarray problems.
- Use it when you're working with a **contiguous segment** and optimizing a result.
- Sliding Window can be **fixed-size** or **variable-sized**, depending on the constraints.
- Often combined with **hash maps**, **sets**, or **counters** to manage the internal window state.

> 🚀 Once you master this technique, many "medium" and even "hard" problems will start to look approachable.

