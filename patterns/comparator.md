``` cpp
// Dijkstra Logic
priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
pq.push({0, startNode}); 

while(!pq.empty()) {
    auto [d, u] = pq.top(); pq.pop();
    if (d > dist[u]) continue;

    for (auto& [v, weight] : adj[u]) {
        // Pivot to A*: newDist = d + weight + heuristic(v, target)
        if (dist[u] + weight < dist[v]) {
            dist[v] = dist[u] + weight;
            pq.push({dist[v], v});
        }
    }
}