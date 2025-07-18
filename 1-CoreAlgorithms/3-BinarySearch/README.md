# 🔎 Binary Search Technique

The **Binary Search** technique is an efficient method for finding elements or values within **sorted data**. It's a fundamental algorithm in computer science and a common pattern for solving **search and optimization problems** in logarithmic time.

---

## 📌 What Is Binary Search?

Binary Search works by **repeatedly dividing the search space in half**. It compares the middle element to the target, and based on the result, **eliminates half of the array** from consideration.

It relies on the key property that the input array or range is **sorted**.

---

## ⚡ Why Use Binary Search?

- Drastically reduces time complexity from **O(n)** to **O(log n)**.
- Applicable in a wide range of problems beyond just searching.
- Works in arrays, search spaces, and even in custom conditions (like binary search on the answer).

---

## 🎯 When to Use Binary Search?

Use Binary Search when:

- You’re working with a **sorted array or list**.
- You’re optimizing over a **monotonic function or range**.
- You're solving for:
  - **Exact matches**
  - **Boundary conditions** (first/last occurrence)
  - **Decision problems** (“can you achieve X under Y?”)

---

## 🧠 Core Idea

1. Define search space with `left` and `right` pointers.
2. Calculate the middle: `mid = (left + right) // 2`.
3. Compare `nums[mid]` with target:
   - Equal → Found
   - Less → Search right half
   - Greater → Search left half
4. Repeat until `left > right`.

---

## 🧩 Binary Search Template

```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if nums[mid] == target:
```


---

## 🔧 Types of Binary Search

| Type                      | Description                             | Example Use Case                                           |
|---------------------------|-----------------------------------------|------------------------------------------------------------|
| **Classic search**        | Find exact element                      | [704. Binary Search](https://leetcode.com/problems/binary-search/) |
| **First/last occurrence** | Search for boundaries with duplicates   | [34. Find First and Last Position](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) |
| **Lower/upper bound**     | Smallest or largest satisfying condition | [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/) |
| **Rotated array**         | Handle rotation in sorted array         | [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) |
| **Binary search on answer** | Search over solution space             | [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) |

---

## 🧪 Common Problems to Practice

| Problem                                                                 | Pattern               |
|-------------------------------------------------------------------------|------------------------|
| [704. Binary Search](https://leetcode.com/problems/binary-search/)     | Classic                |
| [35. Search Insert Position](https://leetcode.com/problems/search-insert-position/) | Lower bound            |
| [34. First and Last Position](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) | First/last occurrence  |
| [33. Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) | Rotated search         |
| [81. Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/) | Rotated + Duplicates   |
| [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/) | Binary search on answer |
| [4. Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) | Advanced binary search |

---

## 💡 Compare All 3 Cases: Return Strategy by Binary Search Type

| Problem Type            | Loop Return      | Purpose                                       |
|-------------------------|------------------|-----------------------------------------------|
| **Exact match (704)**   | `return mid`     | Find any one occurrence                       |
| **Lower bound (35)**    | `return left`    | First element ≥ target (or insertion point)   |
| **Upper bound**         | `return right`   | Last element ≤ target (or last occurrence)    |

---


🎯 Summary
> Use return mid when you only care about existence of a value.

> Use return left when you need the first index ≥ target (lower bound / insert position).

> Use return right when you need the last index ≤ target (upper bound / last occurrence).

> Mastering this return logic is key to solving a wide range of problems using binary search.

