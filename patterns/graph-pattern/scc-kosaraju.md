The Logic:

DFS 1: Sort nodes by finish time (using a stack).

Reverse: Transpose the graph (flip all edge directions).

DFS 2: Process nodes from the stack on the reversed graph. Each DFS tree formed here is an SCC.

The "Naked Truth" on SCCs:

Why Transpose? Fipping the edges ensures that if you start a DFS from a "sink" SCC in the original graph's finish-time order, you won't bleed into other components.

Real-world Use: Used in Social Network Analysis (identifying tight-knit communities) and Garbage Collection (detecting cycles of objects that can be reclaimed).

Condensation Graph: Once you find SCCs, you can treat each SCC as a single node to create a DAG. This is a common follow-up question.
``` cpp
class SCC {
    void dfs1(int u, vector<vector<int>>& adj, vector<bool>& vis, stack<int>& st) {
        vis[u] = true;
        for (int v : adj[u]) {
            if (!vis[v]) dfs1(v, adj, vis, st);
        }
        st.push(u); // Finish time ordering
    }

    void dfs2(int u, vector<vector<int>>& adjRev, vector<bool>& vis, vector<int>& component) {
        vis[u] = true;
        component.push_back(u);
        for (int v : adjRev[u]) {
            if (!vis[v]) dfs2(v, adjRev, vis, component);
        }
    }

public:
    vector<vector<int>> findSCCs(int n, vector<vector<int>>& adj) {
        vector<bool> vis(n, false);
        stack<int> st;

        // Step 1: Fill stack with finish times
        for (int i = 0; i < n; i++) {
            if (!vis[i]) dfs1(i, adj, vis, st);
        }

        // Step 2: Transpose the graph
        vector<vector<int>> adjRev(n);
        for (int u = 0; u < n; u++) {
            for (int v : adj[u]) adjRev[v].push_back(u);
        }

        // Step 3: DFS on reversed graph in order of stack
        fill(vis.begin(), vis.end(), false);
        vector<vector<int>> sccs;
        while (!st.empty()) {
            int u = st.top(); st.pop();
            if (!vis[u]) {
                vector<int> component;
                dfs2(u, adjRev, vis, component);
                sccs.push_back(component);
            }
        }
        return sccs;
    }
};