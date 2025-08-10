
```
max heap - priority_queue<int, vector<int>>mxheap
min heap - priority_queue<int, vector<int>,greater<int>>mnheap

max heap with pair - priority_queue<pair<int,int>, vector<pair<int,int>>>mxheap
min heap with pair -
priority_queue<pair<int,int>, vector<pair<int,int>>,greater<pair<int,int>>>mnheap
```



Certainly! Here's a single piece of code summarizing the creation and usage of both max heaps and min heaps for `pair<int, int>` in C++ STL, including custom comparators based on the second element:

```cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

typedef pair<int, int> pii;

// Comparator for max heap based on the second element of the pair
struct CompareSecondMax {
    bool operator()(const pii &a, const pii &b) {
        return a.second < b.second;
    }
};

// Comparator for min heap based on the second element of the pair
struct CompareSecondMin {
    bool operator()(const pii &a, const pii &b) {
        return a.second > b.second;
    }
};

int main() {
    // Max Heap for pair<int, int>
    priority_queue<pii> maxHeapDefault;
    maxHeapDefault.push({10, 100});
    maxHeapDefault.push({20, 200});
    maxHeapDefault.push({5, 50});
    maxHeapDefault.push({15, 150});
    cout << "Max Heap (default comparator): ";
    while (!maxHeapDefault.empty()) {
        pii top = maxHeapDefault.top();
        cout << "(" << top.first << ", " << top.second << ") ";
        maxHeapDefault.pop();
    }
    cout << endl;

    // Min Heap for pair<int, int>
    priority_queue<pii, vector<pii>, greater<pii>> minHeapDefault;
    minHeapDefault.push({10, 100});
    minHeapDefault.push({20, 200});
    minHeapDefault.push({5, 50});
    minHeapDefault.push({15, 150});
    cout << "Min Heap (default comparator): ";
    while (!minHeapDefault.empty()) {
        pii top = minHeapDefault.top();
        cout << "(" << top.first << ", " << top.second << ") ";
        minHeapDefault.pop();
    }
    cout << endl;

    // Max Heap for pair<int, int> based on second element
    priority_queue<pii, vector<pii>, CompareSecondMax> maxHeapCustom;
    maxHeapCustom.push({10, 100});
    maxHeapCustom.push({20, 200});
    maxHeapCustom.push({5, 50});
    maxHeapCustom.push({15, 150});
    cout << "Max Heap (custom comparator on second element): ";
    while (!maxHeapCustom.empty()) {
        pii top = maxHeapCustom.top();
        cout << "(" << top.first << ", " << top.second << ") ";
        maxHeapCustom.pop();
    }
    cout << endl;

    // Min Heap for pair<int, int> based on second element
    priority_queue<pii, vector<pii>, CompareSecondMin> minHeapCustom;
    minHeapCustom.push({10, 100});
    minHeapCustom.push({20, 200});
    minHeapCustom.push({5, 50});
    minHeapCustom.push({15, 150});
    cout << "Min Heap (custom comparator on second element): ";
    while (!minHeapCustom.empty()) {
        pii top = minHeapCustom.top();
        cout << "(" << top.first << ", " << top.second << ") ";
        minHeapCustom.pop();
    }
    cout << endl;

    return 0;
}
```

### Explanation

1. **Max Heap for `pair<int, int>` (Default Comparator)**
   - Uses the default `priority_queue` which creates a max heap based on the first element of the pair.
2. **Min Heap for `pair<int, int>` (Default Comparator)**
   - Uses `greater<pii>` as the comparator to create a min heap based on the first element of the pair.
3. **Max Heap for `pair<int, int>` Based on Second Element**
   - Uses a custom comparator (`CompareSecondMax`) to create a max heap based on the second element of the pair.
4. **Min Heap for `pair<int, int>` Based on Second Element**
   - Uses a custom comparator (`CompareSecondMin`) to create a min heap based on the second element of the pair.

This code demonstrates how to create and use both max and min heaps with `pair<int, int>` using default and custom comparators.
