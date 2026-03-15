The Logic: 
1. Convert the pattern into a numerical hash value.
2. Slide a window over the text, updating the hash in $O(1)$ by "removing" the high-order digit and "adding" the new low-order digit.
3. Only perform a full string comparison if the hashes match (to handle collisions).

The "Naked Truth" on Collisions

Single Hash vs. Double Hash: In competitive programming or high-stakes interviews, use two different primes (e.g., $10^9+7$ and $10^9+9$) to generate two hashes. The probability of a double collision is nearly zero.
Base Selection: Use a base larger than your alphabet (e.g., 31 for lowercase English, 257 for ASCII).
Why Rabin-Karp for Seniors? It’s the basis for Rsync and Plagiarism Detection. If you’re asked to find if a large file has duplicated chunks, you don't use KMP; you use a rolling hash to fingerprint blocks.

``` cpp
#define MOD 1000000007
#define BASE 31

long long computeHash(string& s, int len) {
    long long h = 0;
    for (int i = 0; i < len; i++) {
        h = (h * BASE + (s[i] - 'a' + 1)) % MOD;
    }
    return h;
}

int rabinKarp(string text, string pattern) {
    int n = text.size(), m = pattern.size();
    if (m > n) return -1;

    long long patternHash = computeHash(pattern, m);
    long long windowHash = computeHash(text, m);

    // Precompute BASE^(m-1) % MOD
    long long maxPow = 1;
    for (int i = 1; i < m; i++) maxPow = (maxPow * BASE) % MOD;

    for (int i = 0; i <= n - m; i++) {
        if (windowHash == patternHash) {
            if (text.substr(i, m) == pattern) return i; // Final check
        }
        
        if (i < n - m) {
            // Rolling the hash:
            // 1. Remove leading char
            windowHash = (windowHash - (text[i] - 'a' + 1) * maxPow) % MOD;
            // 2. Shift left and add trailing char
            windowHash = (windowHash * BASE + (text[i + m] - 'a' + 1)) % MOD;
            // 3. Ensure positive
            if (windowHash < 0) windowHash += MOD;
        }
    }
    return -1;
}