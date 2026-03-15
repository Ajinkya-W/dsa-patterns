``` cpp
// Common "Senior" Bit Tricks
bool isPowerOfTwo(int n) { return n > 0 && (n & (n - 1)) == 0; }

// Get i-th bit: (n >> i) & 1
// Set i-th bit: n | (1 << i)
// Clear i-th bit: n & ~(1 << i)

// Iterating over all subsets of a set (Bitmasking)
for (int i = 0; i < (1 << n); i++) {
    for (int j = 0; j < n; j++) {
        if ((i >> j) & 1) { /* Element j is in subset i */ }
    }
}