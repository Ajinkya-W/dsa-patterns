The Logic: KMP avoids unnecessary re-comparisons by precomputing the LPS (Longest Prefix which is also a Suffix) array. This is essentially building a Finite Automaton to handle "failed" matches gracefully.
``` cpp
vector<int> computeLPS(string pat) {
    int m = pat.length();
    vector<int> lps(m, 0);
    for (int i = 1, j = 0; i < m; i++) {
        while (j > 0 && pat[i] != pat[j]) j = lps[j - 1];
        if (pat[i] == pat[j]) j++;
        lps[i] = j;
    }
    return lps;
}