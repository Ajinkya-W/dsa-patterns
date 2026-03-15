``` cpp
int slidingWindow(vector<int>& nums, int k) {
    int left = 0, right = 0, ans = 0;
    unordered_map<int, int> count;

    for (right = 0; right < nums.size(); right++) {
        // 1. Expand: Add nums[right] to current state
        count[nums[right]]++;

        // 2. Contract: While state is invalid, shrink from left
        while (/* condition violated */) {
            count[nums[left]]--;
            if (count[nums[left]] == 0) count.erase(nums[left]);
            left++;
        }

        // 3. Update: Result is usually the window size
        ans = max(ans, right - left + 1);
    }
    return ans;
}