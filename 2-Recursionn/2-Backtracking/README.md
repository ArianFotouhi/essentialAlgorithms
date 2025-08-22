# 🌌 Backtracking

Backtracking is a problem-solving technique that incrementally builds candidates and abandons ("backtracks" from) a path as soon as it can't possibly lead to a valid solution. It powers classics like N-Queens, permutations/combinations, and Sudoku.

---

## 📌 What is Backtracking?

**Backtracking = DFS + constraints + undo**

You explore choices depth-first, prune invalid paths early using constraints, and revert the state before trying the next choice.

- **Choice:** Pick a candidate move (place a queen, choose a number, include/exclude an element)
- **Constraint/Prune:** If the partial state can't lead to a solution, stop exploring this branch
- **Goal:** When the state is complete and valid, record the solution
- **Undo:** Revert the last move before trying the next

---

## 🧱 Core Template (Python)

```python
def backtrack(state, choices):
    if goal(state):
        record(state)
        return
    for choice in choices_available(state, choices):
        apply(choice, state)         # make move
        if is_valid(state):          # prune early
            backtrack(state, choices)
        revert(choice, state)        # undo move
```

---

## ⚡ Why Use Backtracking?

- Naturally fits combinatorial search over exponential spaces
- Systematic, guarantees you don't miss solutions
- Pruning can turn impossible brute force into tractable search

---

## 🎯 When to Use It

If the problem says **“find all …”**, **“generate all …”**, or **“count all …”**, especially with **constraints**, → backtracking is a strong candidate.

---

## 🛠️ Worked Examples

### 1. N-Queens (place N queens so none attack each other)

Pruning idea: a queen conflicts if another shares column, diag r−c, or anti-diag r+c.

```python
def solveNQueens(n: int):
    cols, diag, anti = set(), set(), set()
    board = [["."] * n for _ in range(n)]
    ans = []

    def backtrack(r: int):
        if r == n:
            ans.append(["".join(row) for row in board])
            return
        for c in range(n):
            if c in cols or (r - c) in diag or (r + c) in anti:
                continue
            cols.add(c); diag.add(r - c); anti.add(r + c)
            board[r][c] = "Q"
            backtrack(r + 1)
            board[r][c] = "."
            cols.remove(c); diag.remove(r - c); anti.remove(r + c)

    backtrack(0)
    return ans
```

**Tips:**
- Use bitmasks for cols/diag/anti to squeeze performance
- Symmetry: mirror solutions to halve search (for even N)

---

## 🧠 Key Concepts

| Concept         | Description                                              |
|-----------------|----------------------------------------------------------|
| State           | The partial solution (board, path, placements)           |
| Choices         | The available moves from current state                   |
| Constraints     | Rules to keep the partial state valid; used for pruning  |
| Pruning         | Stopping early when no completion is possible            |
| Undo (Backtrack)| Revert the last move to try another                      |
| Heuristics      | Ordering choices (MRV, least-constraining value)         |
| Bitmasking      | Fast set checks (e.g., N-Queens columns/diagonals)       |
| Deduping        | Skip same-value branches to avoid duplicate outputs       |

---

## 🧮 Complexity (typical)

- **Permutations of n:** O(n·n!) time, O(n) extra space (path + used)
- **Combinations C(n,k):** O(C(n,k)·k) time
- **N-Queens:** ~O(N!) in worst case; heavy pruning reduces it
- **Sudoku:** Exponential worst case; MRV + constraint sets are essential

---

## 🧩 Practice Problems (LeetCode)

- [N-Queens / 52. N-Queens II](https://leetcode.com/problems/n-queens/)
- [Permutations / 47. Permutations II (duplicates)](https://leetcode.com/problems/permutations-ii/)
- [Combinations / 39. Combination Sum](https://leetcode.com/problems/combination-sum/) / [40. Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)
- [Subsets / 90. Subsets II](https://leetcode.com/problems/subsets-ii/)
- [Sudoku Solver](https://leetcode.com/problems/sudoku-solver/)
- [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/)
- [Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)

---

## 📘 Summary

- Backtracking = DFS over choices + pruning invalid paths + undo
- Use it for combinatorics and constraint problems (N-Queens, permutations, combinations, Sudoku)
- Big wins come from good constraints, smart ordering, and state structures (sets, bitmasks, MRV)

✨ Master these patterns and most searchy interview problems start to feel... mechanical.