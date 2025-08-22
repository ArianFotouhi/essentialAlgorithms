
# DFS (Depth-First Search)

**In-order • Pre-order • Post-order • Tree & Graph essentials**

---

## What is DFS?
DFS explores one branch as deep as possible before backing up and trying the next. It's fundamental for tree traversals, graph exploration, cycle detection, and "generate all ..." tasks (via backtracking).

---

## When to Use DFS

- **Tree properties:** height, balanced, diameter, sum per subtree, validate BST
- **Graph/grid exploration:** count islands/components, path existence, largest region
- **Cycle detection:** directed (back edges), undirected (via parent)
- **Topological reasoning:** post-order on DAGs
- **Generate/list/count all:** subsets, permutations, combinations, parentheses, N-Queens (DFS backtracking)

---

## DFS Orders (for Trees)

- **Pre-order (node → left → right):** Use when you need the node first (e.g., root-to-leaf path, serialization, cloning)
- **In-order (left → node → right):** Use on BSTs for sorted order, k-th smallest
- **Post-order (left → right → node):** Use when the node's answer depends on children (height, diameter, balanced, subtree sums, DP on trees)

*Quick rule: If you need children's info to compute the parent, use post-order.*

---

## DFS vs. Backtracking

- **Plain DFS:** Visit each node/edge once to compute structure or check reachability
- **Backtracking:** DFS over a choice tree, with pruning and an undo step to enumerate valid solutions

---

## Implementation Checklist

- Pick the order (pre/in/post) based on when you need to process the node
- Define the base case (null node / out of bounds / all choices made)
- Decide the state you carry: visited, depth, current path, bounds, counters
- For graphs/grids: mark visited on entry to prevent revisits; for directed graphs, track state (unseen/visiting/done) to spot cycles
- Aggregations: return the facts parents need (e.g., height & isBalanced)
- Backtracking: choose → check/prune → recurse → undo (restore state)
- Stop early when possible (pruning or once the target is found)

---

## Trees vs. Graphs: Key Differences

- **Trees:** No cycles; usually no visited set needed
- **Graphs/grids:** Cycles/common neighbors exist → always track visited
- **Cycle detection:**
	- Directed: use colors (unseen/visiting/done) to detect back edges
	- Undirected: track the parent to distinguish the edge you came from

---

## Complexity

- **Traversal DFS (trees/graphs):** Time O(V + E), Space O(V) (call stack/explicit stack + visited)
- **Backtracking:** Exponential in the number of choices (e.g., subsets 2^n, permutations n!), depth ≈ problem size

---

## Common Pitfalls

- Forgetting visited on graphs/grids → revisits/infinite loops
- Wrong order: using pre-order when the parent needs children's results (should be post-order)
- No undo in backtracking → state leaks across branches
- Missing base cases (especially bounds/obstacles in grids)
- Mixing tree and graph habits (trees rarely need visited; graphs always do)

---

## Practice Problems

- **Trees:** 104 (Max Depth), 110 (Balanced), 543 (Diameter), 98 (Validate BST)
- **Graphs/Grids:** 200 (Number of Islands), 695 (Max Area of Island)
- **Backtracking (generate-all):** 78 (Subsets), 77 (Combinations), 46 (Permutations)
- **DAG / cycles:** 207 (Course Schedule)

---

## Key Takeaways

- DFS = dive deep, then back up
- Choose the right order (pre/in/post) to match the dependency
- Graphs need visited; trees typically don’t
- Backtracking = DFS + prune + undo
- Post-order for subtree DP