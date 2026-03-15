``` CPP
const int MAXN = 1e5 + 5;
int tree[4 * MAXN], lazy[4 * MAXN];

// Push pending updates down to children
void push(int v) {
    if (lazy[v] != 0) {
        tree[2*v] += lazy[v];
        lazy[2*v] += lazy[v];
        tree[2*v+1] += lazy[v];
        lazy[2*v+1] += lazy[v];
        lazy[v] = 0;
    }
}

void update(int v, int tl, int tr, int l, int r, int add) {
    if (l > r) return;
    if (l == tl && r == tr) {
        tree[v] += add;
        lazy[v] += add;
    } else {
        push(v);
        int tm = (tl + tr) / 2;
        update(2*v, tl, tm, l, min(r, tm), add);
        update(2*v+1, tm+1, tr, max(l, tm+1), r, add);
        tree[v] = max(tree[2*v], tree[2*v+1]);
    }
}

// Range Maximum Query
int query(int v, int tl, int tr, int l, int r) {
    if (l > r) return -1e9;
    if (l == tl && r == tr) return tree[v];
    push(v);
    int tm = (tl + tr) / 2;
    return max(query(2*v, tl, tm, l, min(r, tm)),
               query(2*v+1, tm+1, tr, max(l, tm+1), r));
}