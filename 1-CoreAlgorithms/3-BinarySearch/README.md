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
