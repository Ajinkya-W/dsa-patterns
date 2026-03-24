
``` cpp
class DSU{
    vector<int> parent, ranks;
    public:
    DSU(int n){
        parent.resize(n);
        ranks.resize(n, 0);
        for(int i = 0; i < n; i++){
            parent[i] = i;
        }
    }
    int find(int x){
        if(parent[x] == x){
            return x;
        } else{
            return parent[x] = find(parent[x]);
        }
    }
    bool unite(int x, int y){
        int rootX = find(x);
        int rootY = find(y);
        if(rootX == rootY)  return false;
        if(ranks[rootX] > ranks[rootY]){
            parent[rootY] = rootX;
        } else if(ranks[rootX] < ranks[rootY]){
            parent[rootX] = rootY;
        } else{
            parent[rootY] = rootX;
            ranks[rootX]++;
        } 
        return true;  
    }
};
class Solution {
public:
    int numIslands(vector<vector<char>>& grid) {
        int R = grid.size(), C = grid[0].size();
        
        DSU ds(R * C);
        // we go through each bucket and see which can be combined
        int islands = 0;
        for(int r = 0; r < R; r++){
            for(int c = 0; c < C; c++){
                if(grid[r][c] == '1'){ 
                    islands++;

                    int currPosition = r * C + c;
                    int rightPosition = r * C + (c+1);
                    int downPosition = (r+1) * C + c;

                    if(c + 1 < C && grid[r][c + 1] == '1'){
                        if(ds.unite(currPosition, rightPosition)) islands--;
                    }
                    if(r + 1 < R && grid[r + 1][c] == '1'){
                        if(ds.unite(currPosition, downPosition)) islands--;
                    }
                }
            }
        }
        
        return islands;
    }
};

```
Alternate

``` cpp
class Solution {
private:
    void dfsIslands(vector<vector<char>>& grid, int i, int j, vector<vector<bool>> &visited){
        if(i < 0 || j < 0 || i >= grid.size() || j >= grid[0].size() || grid[i][j] == '0' || visited[i][j]){
            return;
        }
        visited[i][j] = 1;
        
        dfsIslands(grid, i-1, j, visited);
        dfsIslands(grid, i+1, j, visited);
        dfsIslands(grid, i, j-1, visited);
        dfsIslands(grid, i, j+1, visited);
    }
public:
    int numIslands(vector<vector<char>>& grid) {
        int islands = 0, row = grid.size(), col = grid[0].size();
        vector<vector<bool>> visited(row, vector<bool>(col, false));
        for(int i = 0; i < row; i++){
            for(int j = 0; j < col; j++){
                if(!visited[i][j] && grid[i][j] == '1'){
                    islands++;
                    dfsIslands(grid, i, j, visited);
                }
            }
        }
        return islands;
    }
};