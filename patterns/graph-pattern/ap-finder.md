Articulation Points (Critical Nodes)
Logic: Node u is an AP if $low[v] \ge time[u]$ (for non-root) or it's a root with $>1$ child.
``` cpp
class APFinder {
    int timer = 1;
    void dfs(int u, int p, vector<int>& time, vector<int>& low, 
             vector<vector<int>>& adj, vector<bool>& isAP) {
        time[u] = low[u] = timer++;
        int children = 0;

        for (auto v : adj[u]) {
            if (v == p) continue;
            if (time[v] == 0) {
                children++;
                dfs(v, u, time, low, adj, isAP);
                low[u] = min(low[u], low[v]);
                // AP Condition (Non-root)
                if (p != -1 && low[v] >= time[u]) isAP[u] = true;
            } else {
                // Back-edge
                low[u] = min(low[u], time[v]);
            }
        }
        // AP Condition (Root)
        if (p == -1 && children > 1) isAP[u] = true;
    }
};