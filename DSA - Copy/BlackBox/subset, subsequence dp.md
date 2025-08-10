
here we use take and not take strategy, 
backtracking is very important and we can use techniques similar to it.


here the difference comes in finding a subset or k subsets, and finding the number of satisfying k subsets.

1. if we have to find one or k  subset/ subsequence  we don't need to go till the end i.e i>=n in base case, we can check if our subset/subsequence is following the required condition then we can return its property  min/max/gcd/count etc.
   
	 i. here with index i, instead of one subset we can maintain multiple subsets.
	 
 ```
        // Dont include this element in any subsequence

        int skip = solve(i + 1, nums, first, second);

  

        // Include this index in the first subsequence

        int take1 = solve(i + 1, nums, __gcd(first, nums[i]), second);

  

        // Include this index in the second subsequence

        int take2 = solve(i + 1, nums, first, __gcd(second, nums[i]));
```







2. Possibility problems- 


```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <unordered_set>

using namespace std;

// Memoization map
unordered_map<int, unordered_map<int, bool>> memo;

// Recursive function to check if sum can be formed
bool canFormSum(const vector<int>& coins, int currentIndex, int currentSum) {
    // Base case: sum of 0 is always achievable
    if (currentSum == 0) return true;

    // If no coins are left or sum becomes negative
    if (currentIndex < 0 || currentSum < 0) return false;

    // Check memo to avoid redundant calculations
    if (memo[currentIndex].count(currentSum)) {
        return memo[currentIndex][currentSum];
    }

    // Include or exclude the current coin
    bool include = canFormSum(coins, currentIndex - 1, currentSum - coins[currentIndex]);
    bool exclude = canFormSum(coins, currentIndex - 1, currentSum);

    // Store result in memo and return
    memo[currentIndex][currentSum] = include || exclude;
    return memo[currentIndex][currentSum];
}

// Function to count unique achievable sums
int countUniqueSums(const vector<int>& coins) {
    int totalSum = 0;
    for (int coin : coins) totalSum += coin;

    unordered_set<int> possibleSums;

    // Check each sum from 0 to totalSum
    for (int sum = 0; sum <= totalSum; sum++) {
        if (canFormSum(coins, coins.size() - 1, sum)) {
            possibleSums.insert(sum);
        }
    }
    return possibleSums.size();  // Count of unique sums
}

int main() {
    vector<int> coins = {1, 3, 3, 5};
    cout << "Number of unique possible sums: " << countUniqueSums(coins) << endl;
    return 0;
}
```
