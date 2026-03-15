``` cpp
struct Event {
    int time;
    int type; // +1 for start, -1 for end

    bool operator<(const Event& other) const {
        if (time != other.time) return time < other.time;
        return type < other.type; // Tie-break logic: process ends before starts?
    }
};

int maxOverlaps(vector<pair<int, int>>& intervals) {
    vector<Event> events;
    for (auto& p : intervals) {
        events.push_back({p.first, 1});
        events.push_back({p.second, -1});
    }
    sort(events.begin(), events.end());

    int active = 0, maxActive = 0;
    for (auto& e : events) {
        active += e.type;
        maxActive = max(maxActive, active);
    }
    return maxActive;
}