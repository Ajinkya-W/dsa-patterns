Logic: At each element, you have two choices: include it or exclude it. This is the foundation for Partition Sum, Coin Change, and Target Sum.
``` cpp
// Space Optimized: O(W) space
int knapsack(vector<int>& weights, vector<int>& values, int W) {
    vector<int> dp(W + 1, 0);
    for (int i = 0; i < weights.size(); i++) {
        // Iterate backwards to avoid using the same item twice
        for (int j = W; j >= weights[i]; j--) {
            dp[j] = max(dp[j], values[i] + dp[j - weights[i]]);
        }
    }
    return dp[W];
}