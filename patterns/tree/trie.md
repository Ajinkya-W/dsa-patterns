``` cpp
struct TrieNode {
    TrieNode* children[26] = {nullptr};
    bool isEnd = false;
};

void insert(string word) {
    TrieNode* curr = root;
    for (char c : word) {
        if (!curr->children[c - 'a']) curr->children[c - 'a'] = new TrieNode();
        curr = curr->children[c - 'a'];
    }
    curr->isEnd = true;
}