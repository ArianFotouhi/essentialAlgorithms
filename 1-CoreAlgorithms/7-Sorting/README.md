# ⚙️ Essential Sorting Algorithms 

Focus on the **4 most practical sorting algorithms**:
- Merge Sort
- Quick Sort
- Heap Sort
- TimSort (Python's built-in)

---

## 📊 Comparison Table

| Algorithm   | Time Complexity (Avg/Worst) | Space  | Stable? | When to Use                            |
|-------------|-----------------------------|--------|---------|----------------------------------------|
| Merge Sort  | O(n log n) / O(n log n)     | O(n)   | ✅      | Stable sort needed, linked list, external sorting |
| Quick Sort  | O(n log n) / O(n²)          | O(log n) | ❌   | Fast in practice, in-place             |
| Heap Sort   | O(n log n) / O(n log n)     | O(1)   | ❌      | Constant space sort, no recursion      |
| TimSort     | O(n log n) / O(n log n)     | O(n)   | ✅      | Default in Python (`sorted()`), real-world data |

---

## 1️⃣ Merge Sort

### 🔧 How It Works:
- Divide the array recursively into halves.
- Sort each half, then **merge** them back in sorted order.
- Uses **extra space** for merging.

### 🧠 When to Use:
- When **stability** is required (e.g., objects with secondary sorting fields).
- On **linked lists** (can be done in-place).
- For **external sorting** (when data doesn't fit in memory).

### 🌟 Key Properties:
- Stable ✅
- Consistent O(n log n) time complexity
- Not in-place (O(n) space)

```
Starting Merge Sort...

Splitting: [5, 2, 8, 1, 3]
  Splitting: [5, 2]
    Returning: [5]
    Returning: [2]
  Start merging:
    Left:  [5]
    Right: [2]
    Comparing: left[0]=5 vs right[0]=2
      → Picked 2 from right
      Result so far: [2]
      → Appending remaining 5 from left
    Finished merge: [2, 5]

  Merging: [5] + [2] => [2, 5]
  Splitting: [8, 1, 3]
    Returning: [8]
    Splitting: [1, 3]
      Returning: [1]
      Returning: [3]
    Start merging:
      Left:  [1]
      Right: [3]
      Comparing: left[0]=1 vs right[0]=3
        → Picked 1 from left
        Result so far: [1]
        → Appending remaining 3 from right
      Finished merge: [1, 3]

    Merging: [1] + [3] => [1, 3]
  Start merging:
    Left:  [8]
    Right: [1, 3]
    Comparing: left[0]=8 vs right[0]=1
      → Picked 1 from right
      Result so far: [1]
    Comparing: left[0]=8 vs right[1]=3
      → Picked 3 from right
      Result so far: [1, 3]
      → Appending remaining 8 from left
    Finished merge: [1, 3, 8]

  Merging: [8] + [1, 3] => [1, 3, 8]
Start merging:
  Left:  [2, 5]
  Right: [1, 3, 8]
  Comparing: left[0]=2 vs right[0]=1
    → Picked 1 from right
    Result so far: [1]
  Comparing: left[0]=2 vs right[1]=3
    → Picked 2 from left
    Result so far: [1, 2]
  Comparing: left[1]=5 vs right[1]=3
    → Picked 3 from right
    Result so far: [1, 2, 3]
  Comparing: left[1]=5 vs right[2]=8
    → Picked 5 from left
    Result so far: [1, 2, 3, 5]
    → Appending remaining 8 from right
  Finished merge: [1, 2, 3, 5, 8]

Merging: [2, 5] + [1, 3, 8] => [1, 2, 3, 5, 8]

Final sorted: [1, 2, 3, 5, 8]
```
---

## 2️⃣ Quick Sort

### 🔧 How It Works:
- Choose a **pivot**, partition the array so smaller elements go left, larger right.
- Recursively apply to left and right subarrays.
- **In-place** (no extra memory for merge step).

### 🧠 When to Use:
- When you need a **fast, in-place** sort.
- When stability is **not required**.
- For most general use cases (e.g., sorting numbers or primitive types).

### ⚠️ Pitfalls:
- Worst case O(n²) if pivot choice is poor (e.g., always smallest/largest element).
- Not stable ❌

### 🌟 Key Properties:
- Fast in practice due to low overhead
- In-place (O(log n) stack space with good pivoting)
- Recursive

```
Starting Quick Sort...

QuickSort on: [4, 1, 7, 3, 2]
Partitioning: [4, 1, 7, 3, 2], Pivot = 2
  Comparing arr[0]=4 < 2
  Comparing arr[1]=1 < 2
    Swapped: [1, 4, 7, 3, 2]
  Comparing arr[2]=7 < 2
  Comparing arr[3]=3 < 2
  Moved pivot to index 1: [1, 2, 7, 3, 4]
After partition: [1, 2, 7, 3, 4] (pivot index 1)

  QuickSort on: [7, 3, 4]
  Partitioning: [7, 3, 4], Pivot = 4
    Comparing arr[2]=7 < 4
    Comparing arr[3]=3 < 4
      Swapped: [1, 2, 3, 7, 4]
    Moved pivot to index 3: [1, 2, 3, 4, 7]
  After partition: [1, 2, 3, 4, 7] (pivot index 3)


Final sorted: [1, 2, 3, 4, 7]
```
---

## 3️⃣ Heap Sort

### 🔧 How It Works:
- Build a **max heap**.
- Repeatedly extract the max and rebuild the heap.
- Done **in-place** (no recursion or extra arrays).

### 🧠 When to Use:
- When **space is limited** (O(1) space).
- In **resource-constrained systems**.
- If **recursion is not allowed** (non-recursive logic).

### ⚠️ Pitfalls:
- Not stable ❌
- Slower than Quick Sort in practice due to more swaps and less cache-friendliness.

### 🌟 Key Properties:
- Deterministic O(n log n)
- In-place
- No recursion
```
Initial array: [3, 9, 4, 1, 7]
🔨 Building max heap...

Heapifying at index 1 (value=9), heap size=5
  Left child index 3, value=1
  Right child index 4, value=7
  No swap needed
Heap after heapify(1): [3, 9, 4, 1, 7]

Heapifying at index 0 (value=3), heap size=5
  Left child index 1, value=9
  Right child index 2, value=4
  -> Swap needed: arr[0]=3 < arr[1]=9
  After swap: [9, 3, 4, 1, 7]
  Heapifying at index 1 (value=3), heap size=5
    Left child index 3, value=1
    Right child index 4, value=7
    -> Swap needed: arr[1]=3 < arr[4]=7
    After swap: [9, 7, 4, 1, 3]
    Heapifying at index 4 (value=3), heap size=5
      No swap needed
Heap after heapify(0): [9, 7, 4, 1, 3]

📦 Extracting elements from heap...

↔️  Swapping root arr[0]=9 with arr[4]=3
  After swap: [3, 7, 4, 1, 9]
Heapifying at index 0 (value=3), heap size=4
  Left child index 1, value=7
  Right child index 2, value=4
  -> Swap needed: arr[0]=3 < arr[1]=7
  After swap: [7, 3, 4, 1, 9]
  Heapifying at index 1 (value=3), heap size=4
    Left child index 3, value=1
    No swap needed
Heap after extraction at index 4: [7, 3, 4, 1, 9]

↔️  Swapping root arr[0]=7 with arr[3]=1
  After swap: [1, 3, 4, 7, 9]
Heapifying at index 0 (value=1), heap size=3
  Left child index 1, value=3
  Right child index 2, value=4
  -> Swap needed: arr[0]=1 < arr[2]=4
  After swap: [4, 3, 1, 7, 9]
  Heapifying at index 2 (value=1), heap size=3
    No swap needed
Heap after extraction at index 3: [4, 3, 1, 7, 9]

↔️  Swapping root arr[0]=4 with arr[2]=1
  After swap: [1, 3, 4, 7, 9]
Heapifying at index 0 (value=1), heap size=2
  Left child index 1, value=3
  -> Swap needed: arr[0]=1 < arr[1]=3
  After swap: [3, 1, 4, 7, 9]
  Heapifying at index 1 (value=1), heap size=2
    No swap needed
Heap after extraction at index 2: [3, 1, 4, 7, 9]

↔️  Swapping root arr[0]=3 with arr[1]=1
  After swap: [1, 3, 4, 7, 9]
Heapifying at index 0 (value=1), heap size=1
  No swap needed
Heap after extraction at index 1: [1, 3, 4, 7, 9]


✅ Final sorted array: [1, 3, 4, 7, 9]
```
---

## 4️⃣ TimSort (Built-in in Python)

### 🔧 How It Works:
- Hybrid of **Merge Sort + Insertion Sort**.
- Detects and exploits **naturally occurring runs** in real-world data.
- Uses **insertion sort for small runs** and **merge sort for larger runs**.

### 🧠 When to Use:
- **Default choice** in Python (`sorted()`, `.sort()`).
- For sorting **real-world messy data**.
- When **stability** matters (e.g., stable multi-key sorts).

### 🌟 Key Properties:
- Stable ✅
- Fast in practice on real-world data
- Optimized for performance and practical cases

```
Initial array: [5, 21, 7, 23, 19, 10, 12, 1, 3, 8]
Insertion sorting from 0 to 9
  Step 1: [5, 21, 7, 23, 19, 10, 12, 1, 3, 8]
  Step 2: [5, 7, 21, 23, 19, 10, 12, 1, 3, 8]
  Step 3: [5, 7, 21, 23, 19, 10, 12, 1, 3, 8]
  Step 4: [5, 7, 19, 21, 23, 10, 12, 1, 3, 8]
  Step 5: [5, 7, 10, 19, 21, 23, 12, 1, 3, 8]
  Step 6: [5, 7, 10, 12, 19, 21, 23, 1, 3, 8]
  Step 7: [1, 5, 7, 10, 12, 19, 21, 23, 3, 8]
  Step 8: [1, 3, 5, 7, 10, 12, 19, 21, 23, 8]
  Step 9: [1, 3, 5, 7, 8, 10, 12, 19, 21, 23]
```

✅ Final sorted array: [1, 3, 5, 7, 8, 10, 12, 19, 21, 23]

```python
# Always use TimSort for general purpose in Python
sorted(arr)          # Returns new sorted list
arr.sort()           # Sorts in place
```


# 🧠 Summary: Which One Should You Use?

| Use Case                          | Recommended Algorithm      |
| --------------------------------- | -------------------------- |
| General-purpose sorting (Python)  | **TimSort**                |
| Need stable sort for complex data | **Merge Sort / TimSort**   |
| Memory-constrained, no recursion  | **Heap Sort**              |
| In-place fast sort (non-stable)   | **Quick Sort**             |
| Sorting linked lists              | **Merge Sort**             |
| Guaranteed performance            | **Merge Sort / Heap Sort** |

## Tip
Unless you're implementing sorting yourself, use:

```python
sorted(arr)          # When you need a new sorted list
arr.sort()           # When you can sort in-place
```

## What does it mean the Stability?
A sorting algorithm is stable if:

> When two elements have the same key (i.e. are equal in sorting criteria), their relative order in the original list is preserved in the sorted list.

example:
```python
people = [
    ("Alice", 25),
    ("Bob", 22),
    ("Charlie", 25),
    ("David", 22)
]
```
sorting by age:
### Stable Sort Result:
```python
[
    ("Bob", 22),     # came before David in the original
    ("David", 22),
    ("Alice", 25),   # came before Charlie in the original
    ("Charlie", 25)
]
```
### Unstable Sort Result 
```python
[
    ("David", 22),   # swapped order
    ("Bob", 22),
    ("Charlie", 25),
    ("Alice", 25)
]
```
> Sorting helps to get predictable, repeatable results.

