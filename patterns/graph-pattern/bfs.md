``` cpp
void bfs(int startNode, vector<vector<int>>& adj) {
    vector<bool> vis(adj.size(), false);
    queue<int> q;

    q.push(startNode);
    vis[startNode] = true;

    while (!q.empty()) {
        int u = q.front(); q.pop();
        // Process node u

        for (int v : adj[u]) {
            if (!vis[v]) {
                vis[v] = true;
                q.push(v);
            }
        }
    }
}