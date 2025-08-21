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

- Generate permutations/combinations/subsets
- Place items with mutual constraints (e.g., N-Queens)
- Solve constraint satisfaction problems (e.g., Sudoku, crosswords)
- Pathfinding with rules (word ladders with constraints, knight's tour, etc.)

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

### 2. Permutations (unique permutations, handle duplicates)

Pruning idea: when nums contain duplicates, avoid generating identical permutations by skipping same value that hasn't been used in this layer.

```python
def permuteUnique(nums):
    nums.sort()
    used = [False] * len(nums)
    path, out = [], []

    def backtrack():
        if len(path) == len(nums):
            out.append(path[:]); return
        prev = None
        for i, x in enumerate(nums):
            if used[i] or x == prev:  # skip dup at this depth
                continue
            used[i] = True; path.append(x)
            backtrack()
            path.pop(); used[i] = False
            prev = x

    backtrack()
    return out
```

### 3. Combinations (n choose k)

Two common styles: choose/skip or for-loop with start index. Add early stop when not enough elements remain.

```python
def combine(n: int, k: int):
    res, path = [], []
    def backtrack(start: int):
        if len(path) == k:
            res.append(path[:]); return
        # pruning: i can go only so far that enough remain
        for i in range(start, n + 1 - (k - len(path)) + 1):
            path.append(i)
            backtrack(i + 1)
            path.pop()
    backtrack(1)
    return res
```

### 4. Sudoku (fill 9×9 so row/col/box each have 1–9)

Pruning idea: maintain candidate sets per row/col/box; always choose the cell with minimum remaining values (MRV).

```python
def solveSudoku(board):
    # board is List[List[str]] with "." for empty
    rows = [set() for _ in range(9)]
    cols = [set() for _ in range(9)]
    boxes = [set() for _ in range(9)]
    empties = []

    for r in range(9):
        for c in range(9):
            v = board[r][c]
            if v == ".":
                empties.append((r, c))
            else:
                rows[r].add(v); cols[c].add(v); boxes[(r//3)*3 + c//3].add(v)

    def candidates(r, c):
        used = rows[r] | cols[c] | boxes[(r//3)*3 + c//3]
        return [str(d) for d in range(1, 10) if str(d) not in used]

    def backtrack():
        if not empties:
            return True
        # MRV heuristic
        idx, (r, c) = min(enumerate(empties), key=lambda t: len(candidates(*t[1])))
        empties[idx], empties[-1] = empties[-1], empties[idx]
        r, c = empties.pop()
        for v in candidates(r, c):
            board[r][c] = v
            rows[r].add(v); cols[c].add(v); boxes[(r//3)*3 + c//3].add(v)
            if backtrack():
                return True
            rows[r].remove(v); cols[c].remove(v); boxes[(r//3)*3 + c//3].remove(v)
            board[r][c] = "."
        empties.append((r, c))
        return False

    backtrack()
    return board
```

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