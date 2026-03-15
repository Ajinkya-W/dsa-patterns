``` cpp
void solve(vector<int>& nums, int target) {
    sort(nums.begin(), nums.end()); // Often required
    int left = 0, right = nums.size() - 1;

    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) {
            // Found pair, move both to find next potential
            left++; right--;
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
}