``` cpp
bool hasCycle(int u, vector<vector<int>>& adj, vector<int>& vis) {
    // vis: 0 = unvisited, 1 = visiting (in stack), 2 = visited
    vis[u] = 1;

    for (int v : adj[u]) {
        if (vis[v] == 1) return true; // Found back-edge (Cycle!)
        if (vis[v] == 0 && hasCycle(v, adj, vis)) return true;
    }

    vis[u] = 2; // Remove from current path stack
    return false;
}