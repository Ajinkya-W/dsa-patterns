# 🧠 DSA Pattern Decision Matrix (Senior Edition)

> **The Naked Truth:** Interviews are won on complexity targets. If you know the constraints, you know the pattern.

---

### **1. Linear & Interval Patterns**
| Pattern | Time | Space | Selection Logic / "Naked Truth" | Link |
| :--- | :--- | :--- | :--- | :--- |
| **Line Sweep** | $O(N \log N)$ | $O(N)$ | Use for static intervals, meeting rooms, and coverage. | [Ref](./linear-pattern/line-sweep.md) |
| **Segment Tree** | $O(\log N)$ | $O(N)$ | Pivot here for **streaming** range updates or $10^9$ ranges. | [Ref](./tree/segment-tree.md) |
| **Sliding Window** | $O(N)$ | $O(1)$ | Best for contiguous subarray constraints. | [Ref](./linear-pattern/sliding-window.md) |
| **Two Pointers** | $O(N)$ | $O(1)$ | Use on **sorted** arrays for pairs/triplets. | [Ref](./linear-pattern/two-pointers.md) |
| **Monotonic Stack** | $O(N)$ | $O(N)$ | Finding "Next Greater/Smaller" in one pass. | [Ref](./monotonic-stack.md) |
| **Prefix Sum** | $O(N)$ | $O(N)$ | $O(1)$ range sum queries after $O(N)$ preprocessing. | [Ref](./linear-pattern/prefix-sum.md) |

---

### **2. Graph & Connectivity Patterns**
| Pattern | Time | Space | Selection Logic / "Naked Truth" | Link |
| :--- | :--- | :--- | :--- | :--- |
| **BFS** | $O(V+E)$ | $O(V)$ | Shortest path in **unweighted** graphs or "K-stops" limits. | [Ref](./graph-pattern/bfs.md) |
| **Dijkstra** | $O(E \log V)$ | $O(V)$ | Shortest path in **weighted** graphs (positive only). | [Ref](./graph-pattern/dijkstra.md) |
| **A* Search** | $O(E \log V)$ | $O(V)$ | Optimized Dijkstra using heuristics (e.g., Manhattan). | [Ref](./graph-pattern/a-star.md) |
| **DSU** | $O(\alpha(N))$ | $O(N)$ | Dynamic connectivity, cycle detection, and Kruskal's. | [Ref](./graph-pattern/dsu.md) |
| **Topo Sort** | $O(V+E)$ | $O(V)$ | Dependency resolution. **Requires a DAG.** | [Ref](./graph-pattern/topo-sort.md) |
| **Cycle (Dir)** | $O(V+E)$ | $O(V)$ | Uses `Recursion Stack` state (Visiting/Visited). | [Ref](./graph-pattern/directed-cycles.md) |
| **Bridges/AP** | $O(V+E)$ | $O(V)$ | Finding critical vulnerabilities (Bridges or Articulation Pts). | [Ref](./graph-pattern/bridge-finder.md) |
| **SCC** | $O(V+E)$ | $O(V+E)$ | Mutual reachability in directed graphs (Kosaraju's). | [Ref](./graph-pattern/scc-kosaraju.md) |

---

### **3. Dynamic Programming (Decision Patterns)**
| Pattern | Time | Space | Selection Logic / "Naked Truth" | Link |
| :--- | :--- | :--- | :--- | :--- |
| **0/1 Knapsack** | $O(N \cdot W)$ | $O(W)$ | "Pick or Don't Pick" decisions with a fixed capacity. | [Ref](./dp-pattern/dp-knapsack.md) |
| **LCS / Sequences**| $O(N \cdot M)$ | $O(\min(N, M))$ | Comparing two strings/sequences (Alignment/Edit Dist). | [Ref](./dp-pattern/dp-sequences.md) |
| **Interval DP** | $O(N^3)$ | $O(N^2)$ | Problems involving merging/splitting (e.g., MCM). | [Ref](./dp-pattern/interval-dp.md) |
| **Bitmask DP** | $O(2^N \cdot N^2)$ | $O(2^N)$ | Optimization for TSP or small $N < 20$ subset states. | [Ref](./dp-pattern/bitmask-dp.md) |
| **Digit DP** | $O(D \cdot S)$ | $O(D \cdot S)$ | Counting numbers in range $[L, R]$ with digit properties. | [Ref](./dp-pattern/digit-dp.md) |

---

### **4. Search, Strings & Optimization**
| Pattern | Time | Space | Selection Logic / "Naked Truth" | Link |
| :--- | :--- | :--- | :--- | :--- |
| **Binary Search** | $O(N \log R)$ | $O(1)$ | Use when the answer space is monotonic (Min-Max). | [Ref](./binary-search-on-answer.md) |
| **QuickSelect** | $O(N)$ avg | $O(1)$ | Finding K-th largest without full sorting. | [Ref](./quick-select.md) |
| **Trie** | $O(L)$ | $O(AL)$ | Prefix matching and dictionary lookups. | [Ref](./tree/trie.md) |
| **KMP / Z-Algo** | $O(N+M)$ | $O(M)$ | Linear string pattern matching (Prefixes/Suffixes). | [Ref](./string-pattern/kmp.md) |
| **Rabin-Karp** | $O(N+M)$ | $O(1)$ | Rolling hash for multiple pattern matching. | [Ref](./string-pattern/robin-karp.md) |

---

### **Critical Constraints & Pivots**
* **$N \le 10^5$**: Usually $O(N \log N)$ or $O(N)$.
* **$N \le 500$**: Could be $O(N^3)$ (Interval DP or Floyd-Warshall).
* **$N \le 20$**: Likely **Backtracking + Pruning** or **Bitmask DP**.
* **Weighted Graph**: **Dijkstra**.
* **Unweighted Graph**: **BFS**.
* **Contiguous Subarray**: **Sliding Window**.