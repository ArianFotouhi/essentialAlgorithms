
# Topological Sort

---

## What is Topological Sort?
Topological Sort orders the nodes of a Directed Acyclic Graph (DAG) so that for every directed edge u → v, node u appears before node v in the ordering.

**Classic approaches:**
- **DFS-based:** Run DFS and push nodes to a stack when finished; reverse stack for order.
- **BFS-based (Kahn’s Algorithm):** Repeatedly pick nodes with in-degree 0, remove them, and reduce neighbors’ in-degree.

---

## When to Use Topological Sort

- **Course Scheduling / Task Ordering:** Prerequisites must be completed first
- **Build Systems / Package Managers:** Dependencies need to be resolved in order
- **Scheduling with Constraints:** Order jobs given precedence constraints
- **Detecting Cycles:** If not all nodes are visited in topo sort, the graph has a cycle

---

## Related Graph Techniques

- **DFS:** Used in topo sort to capture finishing times; also for cycle detection in directed graphs
- **BFS:** Kahn’s algorithm is a BFS on in-degree 0 nodes
- **Union-Find (DSU):** Best for undirected connectivity, not for DAG ordering
- **Topological Sort:** Specialized for DAGs, prerequisite resolution, and dependency ordering

---

## Graph Representations

- **Adjacency List:** Default for storing DAG edges (efficient iteration)
- **Adjacency Matrix:** Rarely used for topo sort, only if graph is small/dense
- **Edge List:** Common input format, usually converted into adjacency list + in-degree array

---

## Key Takeaways

- Use DFS topo sort when recursion/stack fits naturally
- Use BFS (Kahn’s algorithm) when you need in-degree processing or to detect cycles
- Topological sort only works on DAGs — if there’s a cycle, no valid ordering exists