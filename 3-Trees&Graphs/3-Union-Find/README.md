
# Union-Find (Disjoint Set Union, DSU)

---

## What is Union-Find?
Union-Find (DSU) maintains partitions of nodes into disjoint sets, supporting two main operations:
- **Find(x):** Which component does x belong to? (with path compression)
- **Union(x, y):** Merge two components (with union by rank/size)

---

## When to Use Union-Find

- Detect cycles in undirected graphs (if u and v already connected, adding edge forms a cycle)
- Track connected components dynamically
- Build Minimum Spanning Tree (MST) with Kruskal’s algorithm (greedily add edges if they connect different components)

---

## Related Graph Techniques

- **DFS:** Explore as far as possible before backtracking. Good for connected components, cycle detection, path existence, and subtree properties.
- **BFS:** Explore level by level. Great for shortest paths (unweighted), step/time problems, and spreading processes.
- **Topological Sort:** Order nodes in a DAG so every edge u → v has u before v. Used for course scheduling, build systems, dependency resolution.

---

## Graph Representations

- **Adjacency List:** Default, efficient iteration (O(n + m) space)
- **Adjacency Matrix:** For grid-based or dense graphs (O(n²) space)
- **Edge List:** Best for Kruskal’s MST and Union-Find

*Use adjacency lists in most problems unless the grid itself is the graph.*

---

## Key Takeaways

- Use DFS/BFS when you want to explore
- Use DSU when you want to connect & group
- Use Topological Sort when you need an ordering