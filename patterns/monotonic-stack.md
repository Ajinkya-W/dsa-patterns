# Monotonic Stack
*Complexity: O(N) amortized.*

### Use Case
Finding the first element to the left or right that is greater/smaller than the current element.

### Template (Next Greater Element)
```cpp
vector<int> nextGreater(vector<int>& nums) {
    int n = nums.size();
    vector<int> res(n, -1);
    stack<int> st; // Stores indices

    for (int i = 0; i < n; i++) {
        while (!st.empty() && nums[st.top()] < nums[i]) {
            res[st.top()] = nums[i];
            st.pop();
        }
        st.push(i);
    }
    return res;
}