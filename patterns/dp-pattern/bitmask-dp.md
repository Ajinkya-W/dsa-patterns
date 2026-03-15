Logic: Used when $N$ is small (usually $N \le 20$). The state is an integer where the $i$-th bit represents whether element $i$ is used.

``` cpp
int solve(int mask, int last, vector<vector<int>>& dist, vector<vector<int>>& memo) {
    if (mask == (1 << n) - 1) return dist[last][0]; // All visited
    if (memo[mask][last] != -1) return memo[mask][last];

    int res = 1e9;
    for (int next = 0; next < n; next++) {
        if (!(mask & (1 << next))) { // If next not visited
            res = min(res, dist[last][next] + solve(mask | (1 << next), next, dist, memo));
        }
    }
    return memo[mask][last] = res;
}