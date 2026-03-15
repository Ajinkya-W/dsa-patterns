``` cpp
int partition(vector<int>& nums, int left, int right) {
    int pivot = nums[right], fill = left;
    for (int i = left; i < right; i++) {
        if (nums[i] < pivot) swap(nums[i], nums[fill++]);
    }
    swap(nums[fill], nums[right]);
    return fill;
}

int quickSelect(vector<int>& nums, int left, int right, int k) {
    if (left == right) return nums[left];
    int pIndex = partition(nums, left, right);
    if (pIndex == k) return nums[pIndex];
    return pIndex > k ? quickSelect(nums, left, pIndex - 1, k) 
                      : quickSelect(nums, pIndex + 1, right, k);
}