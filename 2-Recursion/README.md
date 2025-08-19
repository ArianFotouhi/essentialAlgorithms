# 🌲 Recursion

Recursion is a fundamental technique in computer science, forming the basis of algorithms like DFS (Depth-First Search), backtracking, and divide-and-conquer. It breaks a problem into smaller subproblems until reaching a base case.

---

## 📌 What is Recursion?

Recursion is when a function calls itself to solve smaller instances of the same problem. It has two main parts:

- **Base Case:** Stops the recursion and prevents infinite loops.
- **Recursive Case:** Breaks the problem into smaller subproblems and calls the function again.

**Example:**

```python
def factorial(n):
    if n == 0:   # Base case
        return 1
    return n * factorial(n - 1)  # Recursive case
```

---

## ⚡ Why Use Recursion?

- Natural fit for problems with self-similar structure (trees, graphs)
- Simplifies complex problems into smaller subproblems
- Reduces boilerplate loops for combinatorial problems

---

## 🎯 When to Use Recursion

Use recursion when:

- The problem can be expressed in terms of smaller subproblems
- There’s a natural tree structure (binary trees, N-Queens, subsets)
- You need DFS traversal (graphs, backtracking)
- Divide-and-conquer algorithms (merge sort, quick sort, binary search)

---

## 🛠️ How It Works

1. Define the base case (the simplest instance of the problem)
2. Break the problem into smaller subproblems
3. Make the recursive call with a smaller input
4. Combine results (if needed)

**Example – Fibonacci:**

```python
def fib(n):
    if n <= 1:   # Base case
        return n
    return fib(n-1) + fib(n-2)  # Recursive case
```

---

## 🧠 Key Concepts

| Concept         | Description                                 |
|-----------------|---------------------------------------------|
| Base Case       | Stopping condition for recursion            |
| Recursive Case  | Calls itself with smaller input             |
| Stack Frames    | Each recursive call uses the call stack     |
| Tail Recursion  | Recursive call is the last operation        |
| Recursion Depth | Max number of nested calls (watch overflow) |

---

## 🧩 Practice Problems

Strengthen your recursion skills with these LeetCode problems:

- [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)
- [784. Letter Case Permutation](https://leetcode.com/problems/letter-case-permutation/)
- [46. Permutations](https://leetcode.com/problems/permutations/)
- [77. Combinations](https://leetcode.com/problems/combinations/)

---

## 📘 Summary

- Recursion = Base case + Recursive case
- Foundation for DFS, backtracking, and divide-and-conquer
- Simplifies problems with self-similar structure
- Essential for solving trees, graphs, and combinatorial problems

✨ Mastering recursion builds the foundation to confidently tackle backtracking, DFS, and advanced divide-and-conquer algorithms.