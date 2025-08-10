```
// Function to find the minimum number of connected sets (distinct intervals)
// we can get if we merge intervals in the given array of intervals
int minimumDivision(vector<int>& startPoints, vector<int>& endPoints, int maxDistance) {
    // Vector to store intervals as pairs [start, end]
    vector<vector<int>> intervals;
    int n =  startPoints.size();
    
    // Creating intervals from given arrays 'startPoints' and 'endPoints'
    for(int i = 0; i < n; i++) {
        intervals.push_back({startPoints[i], endPoints[i]});
    }
    
    // Sorting intervals based on start value
    sort(intervals.begin(), intervals.end());
    
    // Vector to store merged intervals
    vector<vector<int>> mergedIntervals;
    for(int i = 0; i < n; i++) {
        // Add the current interval to the merged intervals
        mergedIntervals.push_back(intervals[i]);
        int j = i;
        // Merge intervals if they overlap
        while(j + 1 < n && mergedIntervals.back()[1] > intervals[j + 1][0]) {
            j++;
        }
        // Update end value of merged interval
        mergedIntervals.back()[1] = max(mergedIntervals.back()[1], intervals[j][1]);
        i = j;
    }

    int mergedSize = mergedIntervals.size();
    int minSets = mergedSize;
    int startIdx = 0, endIdx = 0;
    // Loop through merged intervals to find minimum divisions
    for(int i = 0; i < mergedSize - 1; i++) {
        // Calculate the upper bound for the next interval
        int maxEnd = mergedIntervals[i][1] + maxDistance;
        int low = i + 1;
        int high = mergedSize - 1;
        int nextIdx = low;
        // Binary search to find the farthest interval that can be merged
        // with the current interval under the condition that the end of the merged interval
        // is within 'maxDistance' distance from the end of the current interval
        while(low <= high) {
            int mid = low + (high - low) / 2;
            if(maxEnd >= mergedIntervals[mid][0]) {
                nextIdx = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        // Update answer if current division count is lesser
        if(minSets > i + (mergedSize - nextIdx)) {
            minSets = i + (mergedSize - nextIdx);
            startIdx = i;
            endIdx = nextIdx;
        }
    }
    // Return the minimum division count
    return minSets;
}

```