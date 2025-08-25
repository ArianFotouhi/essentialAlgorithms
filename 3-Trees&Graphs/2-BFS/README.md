
# BFS (Breadth-First Search)

**Level-order • Shortest paths • Layered exploration**

---

## What is BFS?
BFS explores a graph or tree level by level, visiting all neighbors of a node before moving to the next depth. It naturally models “spreading out” from a source and is the foundation of shortest-path algorithms in unweighted graphs.

---

## When to Use BFS

- **Tree traversals:** level-order, zigzag order, bottom-up order
- **Shortest paths (unweighted):** find minimum steps from source to target
- **Connectivity / spreading:** reachability, distances, or the closest resource (nearest leaf, nearest exit)
- **Topological layers:** detect graph levels, bipartite checking
- **Simulation / flooding:** infection spread, word ladder, fire spread

*Quick rule: If you need results grouped by distance/level, use BFS.*

---

## BFS Orders (for Trees)

- **Level-order traversal:** Visit nodes from top to bottom, left to right. Great for problems that care about level grouping (e.g., print by depth, right side view, average per level).
- **Variants:** zigzag (alternate left-right), reverse level-order

---

## BFS vs. DFS

- **BFS:** Explores in “rings” around the source (shallow to deep). Guarantees shortest path in unweighted graphs.
- **DFS:** Explores deeply before backtracking. Useful for recursive dependency problems or subtree properties.

👉 Use BFS when distance or minimum steps matter.
👉 Use DFS when structure or all possible paths matter.

---

## Implementation Checklist

- Use a queue (FIFO)
- For graphs: track visited set to prevent revisiting
- For trees: usually no visited set needed
- Enqueue root/source with level = 0 (or distance = 0)
- While queue not empty:
	- Pop current node
	- Process it (store in level list, update distance, etc.)
	- Push unvisited neighbors/children
- Stop early if target found (shortest path guarantee)

---

## Trees vs. Graphs: Key Differences

- **Trees:** No cycles → no visited set needed
- **Graphs/grids:** Cycles common → always track visited
- **Grids:** Usually store (row, col) in queue + mark visited when enqueued

---

## Complexity

- **Traversal BFS (trees/graphs):** Time O(V + E), Space O(V) for queue + visited
- **Shortest-path BFS:** Same, but may also store parent pointers to reconstruct the path

---

## Common Pitfalls

- Forgetting visited → infinite loops in graphs
- Marking visited too late (enqueue duplicates) → blow up queue
- Off-by-one in distance (is root level 0 or 1?)
- Mixing BFS with weighted graphs (→ need Dijkstra, not plain BFS)

---

## Practice Problems

- **Trees:** 102 (Level Order), 107 (Bottom-Up Level Order), 199 (Right Side View), 637 (Average of Levels)
- **Graphs/Grids:** 1091 (Shortest Path in Binary Matrix), 542 (01 Matrix), 994 (Rotting Oranges), 279 (Perfect Squares)
- **Shortest path / reachability:** 127 (Word Ladder), 752 (Open Lock), 433 (Minimum Genetic Mutation)
- **Bipartite check:** 785 (Is Graph Bipartite)

---

## Key Takeaways

- BFS = explore breadth before depth
- Use for shortest paths and level-order properties
- Trees rarely need visited; graphs always do
- Queue + visited = BFS skeleton
- Stop early if you only need the first target found