``` cpp
// Logic Pivot: Standard Dijkstra PQ stores {dist, node}
// A* PQ stores {f_score, node}
priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;

// Manhattan Distance Heuristic for grid-based pathfinding
int heuristic(int x1, int y1, int x2, int y2) {
    return abs(x1 - x2) + abs(y1 - y2);
}

// Inside the loop:
if (dist_to[u] + weight < dist_to[v]) {
    dist_to[v] = dist_to[u] + weight;
    int f_score = dist_to[v] + heuristic(v, goal);
    pq.push({f_score, v});
}