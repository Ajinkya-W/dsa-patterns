``` cpp
int subarraySum(vector<int>& nums, int k) {
    int count = 0, sum = 0;
    unordered_map<int, int> prevSum;
    prevSum[0] = 1; // Base case: sum of 0 seen once

    for (int n : nums) {
        sum += n;
        // If (sum - k) exists in map, we found a subarray ending here
        if (prevSum.count(sum - k)) count += prevSum[sum - k];
        prevSum[sum]++;
    }
    return count;
}