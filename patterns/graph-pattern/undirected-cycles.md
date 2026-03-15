``` cpp
bool hasCycle(int u, int p, vector<vector<int>>& adj, vector<bool>& vis) {
    vis[u] = true;

    for (int v : adj[u]) {
        if (!vis[v]) {
            if (hasCycle(v, u, adj, vis)) return true;
        } 
        else if (v != p) return true; // Found an already visited node that isn't parent
    }
    return false;
}