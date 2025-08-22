Trees & Graphs — Core Techniques

DFS • BFS • Union-Find (DSU) • Topological Sort • Graph Representations

📌 Mental Model

Tree: acyclic, connected, n-1 edges, usually rooted.

Graph: nodes + edges; may be directed/undirected, weighted/unweighted, cyclic/acyclic.

Representations:

- **Adjacency list (default):** O(n + m) storage; iterate neighbors fast.
- **Adjacency matrix:** O(n^2) storage; constant-time edge lookup.
- **Edge list:** great for DSU/Kruskal.

Use adjacency lists for almost all interview problems unless the matrix/grid itself is the graph.

---

## When to Use What

- **DFS:** components, path existence, subtree DP, cycle detection (directed: color states).
- **BFS:** shortest path (unweighted), levels/steps/time, multi-source spread.
- **DSU:** batch connectivity, cycle in undirected graphs, MST via Kruskal.
- **Topo Sort:** ordering with directed edges and no cycles (DAG).
- **Adj List:** default; Matrix/Grid when the grid is the graph.

---

## Explanations

**DFS (Depth-First Search):**
Explore as far as possible along each branch before backtracking. Useful for path existence, connected components, subtree properties, and cycle detection.

**BFS (Breadth-First Search):**
Explore neighbors level by level. Best for shortest path in unweighted graphs, level order traversal, and multi-source expansion.

**Union-Find (Disjoint Set Union, DSU):**
Efficiently track and merge connected components. Used for cycle detection in undirected graphs, Kruskal’s MST, and dynamic connectivity.

**Topological Sort:**
Order nodes in a directed acyclic graph (DAG) so that for every directed edge u→v, u comes before v. Used for dependency resolution, course scheduling, and task ordering.

**Graph Representations:**
Adjacency lists are the default for most problems. Use matrices when the grid is the graph, and edge lists for algorithms like Kruskal’s MST.