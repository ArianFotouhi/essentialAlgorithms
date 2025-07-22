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

### 🧪 Example (Python):
```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    res = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            res.append(left[i])
            i += 1
        else:
            res.append(right[j])
            j += 1
    res += left[i:]
    res += right[j:]
    return res

arr = [5, 2, 8, 1, 3]
print(merge_sort(arr))  # Output: [1, 2, 3, 5, 8]
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

### 🧪 Example (Python):
```python
def quick_sort(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)
        quick_sort(arr, low, pi - 1)
        quick_sort(arr, pi + 1, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low
    for j in range(low, high):
        if arr[j] < pivot:
            arr[i], arr[j] = arr[j], arr[i]
            i += 1
    arr[i], arr[high] = arr[high], arr[i]
    return i

arr = [4, 1, 7, 3, 2]
quick_sort(arr, 0, len(arr) - 1)
print(arr)  # Output: [1, 2, 3, 4, 7]
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

### 🧪 Example (Python):
```python
def heapify(arr, n, i):
    largest = i
    l = 2*i + 1
    r = 2*i + 2
    if l < n and arr[l] > arr[largest]:
        largest = l
    if r < n and arr[r] > arr[largest]:
        largest = r
    if largest != i:
        arr[i], arr[largest] = arr[largest], arr[i]
        heapify(arr, n, largest)

def heap_sort(arr):
    n = len(arr)
    # Build max heap
    for i in range(n//2 - 1, -1, -1):
        heapify(arr, n, i)
    # Extract elements
    for i in range(n-1, 0, -1):
        arr[i], arr[0] = arr[0], arr[i]
        heapify(arr, i, 0)

arr = [3, 9, 4, 1, 7]
heap_sort(arr)
print(arr)  # Output: [1, 3, 4, 7, 9]
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

```python
# Always use TimSort for general purpose in Python
sorted(arr)          # Returns new sorted list
arr.sort()           # Sorts in place
```

```python
arr = [("b", 2), ("a", 2), ("c", 1)]
# Sort by second item (stable)
arr.sort(key=lambda x: x[1])
print(arr)  # Output: [('c', 1), ('b', 2), ('a', 2)]
# 'b' and 'a' stay in original relative order
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
