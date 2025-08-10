# 1. DP Memoization Mistake: Quick Reference

## The Mistake
- Used 1D array `dp[1000009]` for a function with TWO parameters `f(x, i)`
- Incorrectly saved results as `dp[i] = ans` when `i` was the small value (1-6)
- Result: Constant overwrites, incorrect cached values, wrong answers

## The Fix
- **Match dimensions**: If function is `f(x, i)`, use `dp[MAX_X][MAX_I]`
- **Use consistent indices**: Check and store with same variables
  ```cpp
  if (dp[x][i] != -1) return dp[x][i];
  // ...
  return dp[x][i] = ans;  // Not dp[i]!
  ```

## Quick Checklist
1. ✓ Memoization dimensions = number of state variables
2. ✓ Cache check uses same indices as storage
3. ✓ All recursive states are properly handled
4. ✓ Base cases cover all termination scenarios

## Remember
When you have a function `f(a, b, c)`, you need `dp[a][b][c]` storage - dimensions must match parameters that affect your result!


# 2. DP Mistake: Overlapping Transitions in Dice Sum Problem

## The Mistake
I used three transitions in my recursive DP solution:
```cpp
ans += f(x-i, i) % mod;     // Take dice i, stay at i
ans += f(x-i, i+1) % mod;   // Take dice i, move to i+1 ⚠️ PROBLEM!
ans += f(x, i+1) % mod;     // Don't take dice i, move to i+1
```

**Why it's wrong**: The "take and move" transition creates paths that overlap with "take and stay," causing double counting of the same combinations.

Because in the next function call after "take and stay, " we have the option to "not take and move".



## Example of Double Counting
For sum=8 using dice 1-6:
- Path 1: Take 3, stay → take 3, stay → take 2...
- Path 2: Take 3, move → take 3... 

These can produce the same final combinations, counted twice!

## Correct Approach
Use only two mutually exclusive transitions:
```cpp
// Either USE the current value (and stay)
ans = (ans + f(x-i, i)) % mod;

// OR MOVE to the next value (without using current)
ans = (ans + f(x, i+1)) % mod;
```

## Rule to Remember
For counting problems, transitions must be mutually exclusive to avoid double counting. When modeling choices, each unique outcome should be reachable through exactly one path in your state graph.

# 3. DP Mistake: Permutations vs Combinations in Counting Problems

## The Mistake
I confused **combination counting** (order doesn't matter) with **permutation counting** (order matters) in a dice throw problem.

My recursive approach:
```cpp
// Used i as the current dice value
// f(x-i, i) considered reusing the same value
// f(x, i+1) considered moving to next value
```

This incorrectly counts 1+2 and 2+1 as the SAME pattern.

## How to Identify Similar Problems
- Keywords like "ways to throw a dice," "different sequences," or "orderings"
- Examples that count the same numbers in different orders as distinct solutions
- Problems asking about coin combinations vs coin sequences

## The Correct Approach
For permutation counting (where order matters):
```cpp
// 1D array only tracking the sum
vector<int> dp(n+1, 0);
dp[0] = 1;

for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= 6; j++) { // For each possible dice value
        if (i-j >= 0) {
            dp[i] = (dp[i] + dp[i-j]) % mod;
        }
    }
}


```

```cpp

// 2d array for tracking distinct sums  1+2  & 2+1 are considered same
#include <bits/stdc++.h>
using namespace std;
int dp[1000009][7];
const int mod = 1e9+7;
int f(int x, int i)
{
    // pruning base case
    if(x < 0) return 0;
    if(x == 0) return 1;
    if(i > 6) return 0;  // Consistent with other base cases
    // cache check
    if(dp[x][i] != -1) return dp[x][i];
    // transition
    int ans = 0;
    ans = (ans + f(x-i, i)) % mod;  // Apply modulo after addition
    ans = (ans + f(x, i+1)) % mod;  // Apply modulo after addition
    // save and return
    return dp[x][i] = ans;  // No need for another modulo here
}
int main() {
    int n; cin >> n;
    memset(dp, -1, sizeof(dp));
    cout << f(n, 1);
    return 0;
}
```
## Quick Check
Ask yourself: "Does 1+2 = 2+1 in this problem?"
- If same → Use approach that tracks values (my original mistake)
- If different → Use 1D DP that only tracks the sum