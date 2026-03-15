``` cpp
vector<int> topoSort(int n, vector<vector<int>>& adj) {
    vector<int> inDegree(n, 0);
    // 1. Calculate In-Degrees
    for (int i = 0; i < n; i++) {
        for (int neighbor : adj[i]) {
            inDegree[neighbor]++;
        }
    }

    // 2. Queue all nodes with 0 dependencies
    queue<int> q;
    for (int i = 0; i < n; i++) {
        if (inDegree[i] == 0) q.push(i);
    }

    vector<int> result;
    while (!q.empty()) {
        int curr = q.front(); q.pop();
        result.push_back(curr);

        // 3. For each neighbor, "remove" the dependency
        for (int neighbor : adj[curr]) {
            inDegree[neighbor]--;
            if (inDegree[neighbor] == 0) {
                q.push(neighbor);
            }
        }
    }

    // 4. Cycle Detection: If result size < n, a cycle exists
    if (result.size() != n) return {}; 
    return result;
}