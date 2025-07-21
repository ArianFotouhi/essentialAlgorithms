# 📊 Difference Array Technique

The **Difference Array** technique is a powerful method for solving problems involving **range updates** in arrays efficiently. It's particularly useful for **reducing time complexity from O(n * m) to O(n + m)** in problems with many update operations.

It's a favorite in **LeetCode, coding interviews**, and **competitive programming**.

---

## 📌 What is the Difference Array?

A **Difference Array** `diff[]` is a helper array that lets you efficiently apply changes to a **range of elements** in another array.

Given an original array `arr[]`, the difference array is defined as:

```bash
diff[0] = arr[0]
diff[i] = arr[i] - arr[i-1] for i > 0
```

From the difference array, the original array can be recovered by a **prefix sum**:

```bash
arr[0] = diff[0]
arr[i] = arr[i-1] + diff[i]
```
---

## ⚡ Why Use Difference Array?

- ✅ Perform **range updates in O(1)** time
- ✅ Construct the final array in **O(n)** time using prefix sums
- ✅ Drastically improves performance over naive element-by-element updates

---

## 🎯 When to Use Difference Array?

Use this technique when:

- You're repeatedly updating a **range of indices** in an array
- You need to **add or subtract a value to/from multiple positions**
- The total number of updates is large, but the array size is fixed

---

## 🛠️ How It Works

To **add `val` to a subarray from index `l` to `r` inclusive**:

```python
diff[l] += val
if r + 1 < len(diff):
    diff[r + 1] -= val
```

Then, use a prefix sum on **diff[]** to get the final array.


## 🧠 Key Concepts

| Concept               | Description                                 |
| --------------------- | ------------------------------------------- |
| **Range Update**      | Add `val` to a range `[l, r]` in O(1)       |
| **Cancel the Effect** | Subtract `val` at `r + 1` to limit range    |
| **Prefix Sum**        | Used to reconstruct the final updated array |


## 🧩 Practice Problems

Master the Difference Array technique with these LeetCode problems:

- [Leetcode 1109 – Corporate Flight Bookings](https://leetcode.com/problems/corporate-flight-bookings/)
- [Leetcode 370 – Range Addition](https://leetcode.com/problems/range-addition/)
- [Leetcode 1094 – Car Pooling](https://leetcode.com/problems/car-pooling/)

---

## 📘 Summary

- ✅ **Difference Array** allows efficient range updates using only start and end markers.
- ✅ Great for problems with **many range modifications**.
- ✅ Combine with **prefix sums** to construct final answers quickly.

> ✨ Mastering Difference Array helps crack many **medium-hard array update** problems with confidence and optimal performance.
