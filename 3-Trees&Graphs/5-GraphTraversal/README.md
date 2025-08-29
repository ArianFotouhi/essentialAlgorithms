
# Graph Traversal (Adjacency List / Matrix)

---

## What is Graph Traversal?
Graph traversal means systematically visiting all vertices and edges of a graph. It's the foundation for pathfinding, connectivity, and many graph algorithms.

---

## Graph Representations
- **Adjacency List:** Stores neighbors of each node. Efficient for sparse graphs and easy neighbor iteration.
- **Adjacency Matrix:** 2D matrix where matrix[u][v] = 1 if an edge exists. Best for dense graphs or when edge existence checks are frequent (O(1)).
- **Edge List:** Common input form, often converted before traversal.

---

## Classic Traversal Approaches
- **DFS (Depth-First Search):** Explores as deep as possible along one branch before backtracking. Useful for cycle detection, connected components, and path existence.
- **BFS (Breadth-First Search):** Explores level by level, ensuring shortest path in unweighted graphs. Useful for shortest distances and connectivity checks.

---

## When to Use Graph Traversal
- **Pathfinding in Unweighted Graphs:** BFS gives shortest paths
- **Connectivity Problems:** Determine if the graph is fully connected or count connected components
- **Cycle Detection:** DFS can check for cycles in directed/undirected graphs
- **Flood Fill / Island Problems:** Traverse regions in grids (treated as graphs)
- **Reachability Queries:** Check if a node can reach another node

---

## Related Graph Techniques
- **Union-Find (DSU):** Alternative for connectivity in undirected graphs
- **Topological Sort:** Specialized traversal for DAGs with ordering constraints
- **Dijkstra / Bellman-Ford / Floyd-Warshall:** Extend traversal for weighted shortest paths
- **A* Search:** Heuristic-based pathfinding (common in AI/games)

---

## Key Takeaways
- **DFS:** Explore deep paths, cycle detection, components
- **BFS:** Level-order exploration, shortest path in unweighted graphs
- Choose Adjacency List for most graph problems
- Use Adjacency Matrix only when graph is dense or for quick edge lookups
- Traversal underpins pathfinding, connectivity, and higher-level graph algorithms