``` cpp
bool check(vector<int>& nums, int mid, int k) {
    // Logic to see if 'mid' value is feasible
    // Returns true or false
}

int solve(vector<int>& nums, int k) {
    int low = /* min possible answer */, high = /* max possible answer */;
    int ans = high;
    
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (check(nums, mid, k)) {
            ans = mid;    // Record potential answer
            high = mid - 1; // Try for a smaller/better value
        } else {
            low = mid + 1;
        }
    }
    return ans;
}