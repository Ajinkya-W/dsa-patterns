``` cpp
#include <vector>
#include <numeric>

using namespace std;

class DSU {
public:
    vector<int> parent;
    vector<int> rank; // Height of the tree
    vector<int> size; // Number of nodes in the component
    int numComponents;

    DSU(int n) {
        parent.resize(n + 1);
        iota(parent.begin(), parent.end(), 0); // parent[i] = i
        rank.resize(n + 1, 0);
        size.resize(n + 1, 1);
        numComponents = n;
    }

    // Path Compression: Amortized O(alpha(N))
    int find(int i) {
        if (parent[i] == i) return i;
        return parent[i] = find(parent[i]);
    }

    // 1. Union by Rank: Keeps tree flat by comparing height
    bool unionByRank(int i, int j) {
        int root_i = find(i);
        int root_j = find(j);
        if (root_i == root_j) return false;

        if (rank[root_i] < rank[root_j]) {
            parent[root_i] = root_j;
        } else if (rank[root_i] > rank[root_j]) {
            parent[root_j] = root_i;
        } else {
            parent[root_i] = root_j;
            rank[root_j]++;
        }
        numComponents--;
        return true;
    }

    // 2. Union by Size: Keeps tree flat by comparing node count
    bool unionBySize(int i, int j) {
        int root_i = find(i);
        int root_j = find(j);
        if (root_i == root_j) return false;

        if (size[root_i] < size[root_j]) {
            parent[root_i] = root_j;
            size[root_j] += size[root_i];
        } else {
            parent[root_j] = root_i;
            size[root_i] += size[root_j];
        }
        numComponents--;
        return true;
    }

    // Utility: O(alpha(N))
    int getComponentSize(int i) {
        return size[find(i)];
    }

    bool isConnected(int i, int j) {
        return find(i) == find(j);
    }
};