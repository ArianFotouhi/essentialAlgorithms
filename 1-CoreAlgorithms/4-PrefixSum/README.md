# 📊 Prefix Sum / Difference Array

## ✅ What is Prefix Sum?
The **Prefix Sum** technique precomputes the sum of elements from the beginning of an array up to each index.

This allows you to:
- Query the sum of any subarray in **O(1)** time after **O(n)** preprocessing.
- Avoid recalculating repeated ranges.

---

## 🔧 Prefix Sum Definition:
Given an array `arr`, define `prefix[i]` as:

```python
prefix[i] = arr[0] + arr[1] + ... + arr[i]
```
Or with 1-based indexing:

python
```
prefix[0] = 0
prefix[i] = prefix[i-1] + arr[i-1]
```
🧠 Key Idea:
To get the sum from index l to r:

```python
# 1-based indexing
sum[l:r] = prefix[r] - prefix[l-1]

# 0-based indexing
sum[l:r] = prefix[r] - prefix[l-1]

```

## 💡 When to Use Prefix Sum
Use the prefix sum technique when:

- You need to answer multiple subarray sum queries efficiently.

- You want to avoid recalculating the same subarray sums.

- You're dealing with problems involving cumulative sums or frequencies of sums.

- Prefix sum is ideal for optimizing brute-force approaches where you would otherwise loop over each subarray to compute sums.



# ✅ Prefix Sum: Example, Code, and Use Cases

## ✅ Example

```python
arr = [2, 4, 6, 8, 10]
prefix = [2, 6, 12, 20, 30]

# Sum from index 1 to 3 → 4 + 6 + 8 = 18
# Using 0-based indexing:
prefix[3] - prefix[0] = 20 - 2 = 18
```

## ⚙️ Prefix Sum Code Example
```python
def prefix_sum(arr):
    prefix = [0] * len(arr)
    prefix[0] = arr[0]
    
    for i in range(1, len(arr)):
        prefix[i] = prefix[i - 1] + arr[i]
    
    return prefix
```


## 🧪 Common Prefix Sum Problems
| Problem                              | Idea                    |
| ------------------------------------ | ----------------------- |
| 303. Range Sum Query - Immutable     | Classic prefix sum      |
| 560. Subarray Sum Equals K           | Prefix sum + hash map   |
| 1248. Count Number of Nice Subarrays | Frequency of prefix sum |


