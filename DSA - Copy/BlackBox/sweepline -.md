

QUESTIONS LIST - https://leetcode.com/problem-list/o1qf3c31/
tutorial - https://www.youtube.com/watch?v=QBQvTjNaIRw

ye tab lagta hai jab hame kuch intervals diye ho, aur sweepline hame ye find karne ki madat karta hai
1. ki kisi range me i.e between x and y kitne intervals overlap karrahe hai. 
2. kisi point p par kitne intervals active hai.

![[{E5D55AC2-7B01-4DF2-93A3-CDB0B172D645}.png]]

jaise ki 1-3 ki range me 2 intervals hai i.e [1-7] and [1-6]
jaise ki 3-6 ki range me 3 intervals hai i.e [1-7], [3-8] and [1-6]

![[{74F5FE7E-6DD9-4018-B3B6-1622F3F6BDD4}.png]]

sweepline me hame ek array precompute karke rakhna padta hai, i.e
hame ek array banana hai partials sum, then prefix sum on partial sum array ka use karke, aur is array ke index number line represent karte hai , aur arr[i] matlab number line me ith number par kitne intervals present hai.

Isi ko brute force sweepline bolte hai.
![[{6EC6B4C3-EB79-46B1-BCEC-50CB2C738D49}.png]]


Par question me aisa bhi ho sakta hai ki koi ek interval outlier jaisa ho, to hame bahut bada array bana pad jayega , so isse bachne ke liye hame optimized sweepline use karna padta hai.

![[{9E24EFD8-0B81-447B-AC0C-244F8E71A9A1}.png]]

optimized sweepline me hame array ki gajah map use karna padta hai, aur map me partial array banane wali step tak sab simple hai , example hamare paas ek interval hai [a,b] to ham map ko update karenge aise , mp[a]+=1, mp[b+1]-=1 

par jab ham prefix sum calculate karenge map me to wo thoda trickly hai, hame ek naya map banana hoga i.e prefixmap,  hame maps ke elements par sorted order me traverse karna hoga , aur ye c++ me automatically hota hai, then hame activeinterval ka count maintain karke rakhna hoga 

![[{8E67C755-BB93-47D8-BE48-150823D76EF0}.png]]

In the optimized sweepline algorithm, when we use a `map` (or `std::map` in C++ or `TreeMap` in Java) instead of a regular array to mark the start and end points of intervals, the idea is to efficiently store only the points where an interval starts or ends. This helps in saving space because we avoid creating a large array representing the entire number line, which can be inefficient for large ranges. However, when using a map, performing a prefix sum becomes a bit different, but the logic remains similar.

### Steps to Implement Sweepline Algorithm with a Map:
1. **Mark Interval Boundaries**:
   - Use a map to mark the start and end of intervals.
   - For each interval `[l, r]`, increase the count at `l` (start point) by `1` and decrease the count at `r + 1` (end point) by `1`.

2. **Partial Sum in the Map**:
   - After marking the boundaries, perform a sweep over the map in sorted order of the keys (which represent the important points on the number line).
   - Maintain a running sum while iterating through the map. This running sum will act as the prefix sum, which tells you how many intervals are currently active at each point.

3. **Answer Queries Efficiently**:
   - For any query `[l, r]`, you will use the map to find the prefix sum at `r` and subtract the prefix sum at `l - 1`. Since the map gives you sorted keys, you can find the required sum by performing a sweep up to the range `[l, r]`.

### Code Implementation in C++:

```cpp
#include <iostream>
#include <map>
using namespace std;

int main() {
    // Example intervals: { [1, 5], [2, 6], [4, 8] }
    map<int, int> sweep;

    // Step 1: Mark the start and end points of each interval
    vector<pair<int, int>> intervals = {{1, 5}, {2, 6}, {4, 8}};
    for (auto interval : intervals) {
        sweep[interval.first] += 1;     // Start of interval, increment
        sweep[interval.second + 1] -= 1; // End of interval, decrement
    }

    // Step 2: Perform a prefix sum to calculate how many intervals are active at each point
    int activeIntervals = 0;
    map<int, int> prefixSum; // To store the number of active intervals at each point
    for (auto &[point, value] : sweep) {
        activeIntervals += value;
        prefixSum[point] = activeIntervals;
    }

    // Now we have the prefix sum stored in 'prefixSum' map
    // Step 3: Answer queries
    // Query format: How many intervals are present in the range [l, r]?
    auto getActiveIntervals = [&](int point) -> int {
        // Function to get the value at or just before 'point' in the prefixSum map
        auto it = prefixSum.upper_bound(point); // Find first element greater than point
        if (it == prefixSum.begin()) return 0;  // No element smaller or equal to point
        --it;
        return it->second;
    };

    // Example query: How many intervals are present in [3, 7]?
    int l = 3, r = 7;
    int result = getActiveIntervals(r) - getActiveIntervals(l - 1);
    cout << "Number of intervals in range [" << l << ", " << r << "] = " << result << endl;

    return 0;
}
```

### Explanation:

1. **Marking Intervals**:
   - We iterate through each interval and add `1` at the start of the interval (`l`) and subtract `1` just after the end (`r + 1`).
   - For example, for the interval `[1, 5]`, we mark `1` in the map with `+1` and `6` with `-1`.

2. **Prefix Sum Calculation**:
   - We traverse the `map` (which is ordered by keys) and maintain a running sum (`activeIntervals`) that keeps track of how many intervals are active at each point on the number line.
   - We store this running sum in another map (`prefixSum`) so that for any point `x`, `prefixSum[x]` gives us the number of active intervals at point `x`.

3. **Answering Queries**:
   - To answer a query `[l, r]`, we need to find the number of intervals active up to `r` (`getActiveIntervals(r)`) and subtract the number of intervals active just before `l` (`getActiveIntervals(l - 1)`).

   - The helper function `getActiveIntervals` uses `upper_bound` to efficiently find the prefix sum value just before or equal to the point `r` or `l - 1`.

### Time Complexity:
- **Insertion of intervals**: Each interval adds two operations in the map, so it’s `O(n log n)` where `n` is the number of intervals.
- **Prefix sum calculation**: Since we traverse the map of endpoints, this takes `O(m log m)`, where `m` is the number of distinct endpoints (keys in the map).
- **Querying**: Each query can be answered in `O(log m)` because we are using a map to find the nearest points efficiently.

This approach is very efficient when the number of distinct endpoints (`m`) is much smaller than the total possible points on the number line, making it much better in terms of space complexity than using an array.