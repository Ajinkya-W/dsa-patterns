Bridges (Critical Connections)
the correct implementation strategy. Using two arrays—one for discovery time (the tick at which the node was first hit) and one for low (the minimum discovery time reachable via a back-edge)—is the gold standard.
Logic: 
An edge $(u, v)$ is a bridge if $low[v] > time[u]$.
``` cpp
class BridgeFinder {
    int timer = 1;
    void dfs(int u, int p, vector<int>& time, vector<int>& low, 
             vector<vector<int>>& adj, vector<vector<int>>& bridges) {
        time[u] = low[u] = timer++;
        
        for (auto v : adj[u]) {
            if (v == p) continue;
            if (time[v] == 0) { // Not visited
                dfs(v, u, time, low, adj, bridges);
                low[u] = min(low[u], low[v]);
                // Bridge Condition
                if (low[v] > time[u]) {
                    bridges.push_back({u, v});
                }
            } else {
                // Back-edge: v is an ancestor
                low[u] = min(low[u], time[v]);
            }
        }
    }
public:
    vector<vector<int>> findBridges(int n, vector<vector<int>>& adj) {
        vector<int> time(n, 0), low(n, 0);
        vector<vector<int>> bridges;
        for (int i = 0; i < n; i++) {
            if (time[i] == 0) dfs(i, -1, time, low, adj, bridges);
        }
        return bridges;
    }
};