``` cpp
void backtrack(int start, vector<int>& curr, vector<vector<int>>& res) {
    if (/* goal reached */) {
        res.push_back(curr);
        return;
    }
    for (int i = start; i < options.size(); i++) {
        if (/* pruning condition */) continue; 
        
        curr.push_back(options[i]); // Choose
        backtrack(i + 1, curr, res); // Explore
        curr.pop_back();            // Un-choose (Backtrack)
    }
}