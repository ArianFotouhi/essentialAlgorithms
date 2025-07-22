# 📦 Hashing (HashMap / HashSet)

## 🔍 What is Hashing?

Hashing is a technique to map data (usually keys) to a specific memory location using a **hash function**. It allows for **constant time (O(1))** access on average.

## 🧱 Core Data Structures

- **HashMap** (`dict` in Python): Stores key-value pairs.
- **HashSet** (`set` in Python): Stores only unique keys, no values.

---

## 🧠 Big Picture – Why Use Hashing?

| Use Case            | Why Hashing Helps                        |
|---------------------|------------------------------------------|
| Fast lookup         | O(1) access time (average case)          |
| Duplicate detection | Sets track seen items efficiently        |
| Counting frequencies| Maps associate counts with items         |
| Grouping data       | Group by values or computed keys         |
| Caching             | Store previously computed results        |

---

## 🧭 When to Use HashMap/HashSet?

| Situation                        | Use          |
|----------------------------------|--------------|
| Check if element exists          | `HashSet`    |
| Count occurrences                | `HashMap`    |
| Track visited elements           | `HashSet`    |
| Group data by key or property    | `HashMap`    |
| Cache function calls or results  | `HashMap`    |

---

## 📚 Common LeetCode Patterns

| Pattern                 | Problem Example                                                                 | Core Idea                               |
|-------------------------|----------------------------------------------------------------------------------|------------------------------------------|
| Duplicate detection     | [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)         | Use `HashSet` to track seen items        |
| Frequency counting      | [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)| Count with `HashMap`, sort by freq       |
| Lookup with condition   | [Two Sum](https://leetcode.com/problems/two-sum/)                                | Store complements in `HashMap`           |
| Unique sliding window   | [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) | Use `HashSet` for sliding uniqueness     |
| Grouping                | [Group Anagrams](https://leetcode.com/problems/group-anagrams/)                  | Group by sorted word or frequency tuple  |

---

## ⏱️ Time Complexities

| Operation | HashMap/Set (avg) | HashMap/Set (worst) |
|-----------|-------------------|----------------------|
| Insert    | O(1)              | O(n) (due to collisions) |
| Search    | O(1)              | O(n) |
| Delete    | O(1)              | O(n) |

> ⚠️ Worst-case happens when many keys hash to the same bucket. Still rare in practice.

---

## 🛠️ Quick Coding Patterns

### Count Frequencies
```python
from collections import defaultdict

count = defaultdict(int)
for x in nums:
    count[x] += 1
```

---

## Set for Fast Lookup

```python
seen = set()
for x in nums:
    if x in seen:
        # Duplicate found
        ...
    seen.add(x)
```

---

## Summary
- Use HashMap when you need key-value association.

- Use HashSet to track uniqueness or seen values.

- Hashing helps reduce time complexity to O(1) (avg).

- Crucial for solving lookup, frequency, grouping, and caching problems efficiently.

