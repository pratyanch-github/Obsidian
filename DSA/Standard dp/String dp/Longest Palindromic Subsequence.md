Sure! Below are the **three approaches** we discussed for solving the **Longest Palindromic Subsequence** problem.

### 1. **Recursive Approach with Memoization (Top-Down)**

This approach uses recursion to break the problem into smaller subproblems and memoizes the results to avoid recomputation.

 `dp[i][j] = lps between i and j

```
   if s[i] == s[j] , dp[i][j] = dp[i+1][j-1]
   else dp[i][j] = max( dp[i+1][j], dp[i][j-1]) 
```

 `

 #### Code:
```cpp
class Solution {
public:
    int dp[1001][1001]; // Memoization table
    
    int lps(int i, int j, string &s) {
        // Base cases
        if (i == j) return 1;  // Single character is a palindrome of length 1
        if (i > j) return 0;   // If i crosses j, it's an invalid substring

        // Cache check
        if (dp[i][j] != -1) return dp[i][j];

        // Transitions
        int ans = 0;
        if (s[i] == s[j]) {
            ans = lps(i + 1, j - 1, s) + 2;  // If characters match, extend palindrome
        } else {
            ans = max(lps(i + 1, j, s), lps(i, j - 1, s));  // Otherwise, exclude one character at a time
        }

        return dp[i][j] = ans;
    }

    int longestPalindromeSubseq(string s) {
        memset(dp, -1, sizeof(dp));  // Initialize memoization table with -1
        return lps(0, s.length() - 1, s);  // Call the recursive function
    }
};
```

#### Explanation:
- **Base cases**:
  - If `i == j`, we are looking at a single character which is always a palindrome.
  - If `i > j`, this means the range is invalid, so we return 0.
- **Memoization**: Before computing a result for a subproblem `lps(i, j)`, we check if it's already computed in `dp[i][j]`.
- **Recursive relations**:
  - If `s[i] == s[j]`, extend the palindrome by 2.
  - Otherwise, take the maximum of excluding either `i` or `j`.

#### Time Complexity: O(n^2)
#### Space Complexity: O(n^2) (due to the memoization table)


---

### 2. **Iterative Approach Using `length`**

This approach builds the DP table iteratively using a `length` variable to track the length of the substring being considered. It ensures that smaller substrings are solved first before moving to larger ones.

#### Code:
```cpp
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int n = s.size();
        vector<vector<int>> dp(n, vector<int>(n, 0));  // DP table initialized to 0

        // Base case: Single character substrings are palindromes of length 1
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }

        // Fill the DP table using the `length` of the substring
        for (int length = 2; length <= n; length++) {
            for (int i = 0; i <= n - length; i++) {
                int j = i + length - 1;  // Endpoint of the substring
                if (s[i] == s[j]) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;  // If characters match, extend palindrome
                } else {
                    dp[i][j] = max(dp[i + 1][j], dp[i][j - 1]);  // Otherwise, take the maximum of excluding either end
                }
            }
        }

        // The result is in dp[0][n-1], which represents the longest palindromic subsequence for the entire string
        return dp[0][n - 1];
    }
};
```

#### Explanation:
- **Base case**: Any single character is a palindrome of length 1, so `dp[i][i] = 1` for all `i`.
- **Iterative logic**:
  - We use a `length` variable to represent the length of the current substring.
  - For each substring of length `2` to `n`, we calculate the value of `dp[i][j]`.
  - If `s[i] == s[j]`, then `dp[i][j]` is `2 + dp[i+1][j-1]`.
  - If `s[i] != s[j]`, then `dp[i][j]` is the maximum of excluding either `i` or `j`.

#### Time Complexity: O(n^2)
#### Space Complexity: O(n^2)


---

### 3. **Iterative Approach Using Only `i` and `j`**

This approach uses only the indices `i` and `j` to directly compute the DP table values without explicitly introducing a `length` variable. It ensures that smaller subproblems are solved before larger ones.

#### Code:
```cpp
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int n = s.size();
        vector<vector<int>> dp(n, vector<int>(n, 0));  // DP table initialized to 0

        // Base case: Single character substrings are palindromes of length 1
        for (int i = 0; i < n; i++) {
            dp[i][i] = 1;
        }

        // Fill the DP table using `i` and `j` (directly representing start and end of the substring)
        for (int i = n - 1; i >= 0; i--) {  // Iterate backwards for the start of the substring
            for (int j = i + 1; j < n; j++) {  // j starts after i, representing the end of the substring
                if (s[i] == s[j]) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;  // If characters match, extend palindrome
                } else {
                    dp[i][j] = max(dp[i + 1][j], dp[i][j - 1]);  // Otherwise, take the maximum of excluding either end
                }
            }
        }

        // The result is in dp[0][n-1], which represents the longest palindromic subsequence for the entire string
        return dp[0][n - 1];
    }
};
```

#### Explanation:
- **Base case**: Same as before—any single character is a palindrome of length 1.
- **Iterative logic**:
  - We iterate over all possible substrings by using two indices `i` (start) and `j` (end).
  - The logic to fill `dp[i][j]` is identical to the second approach: if `s[i] == s[j]`, we extend the palindrome by 2; otherwise, we take the maximum of excluding `i` or `j`.
  
#### Time Complexity: O(n^2)
#### Space Complexity: O(n^2)


---

### Summary of Approaches:

| Approach                                | Time Complexity | Space Complexity | Key Idea                                                 |
|-----------------------------------------|-----------------|------------------|----------------------------------------------------------|
| **Recursive with Memoization (Top-Down)**| O(n^2)          | O(n^2)           | Solve subproblems recursively, caching results to avoid recomputation. |
| **Iterative with `length`**             | O(n^2)          | O(n^2)           | Solve iteratively using substring lengths in increasing order. |
| **Iterative with `i` and `j`**          | O(n^2)          | O(n^2)           | Solve iteratively using start (`i`) and end (`j`) indices directly. |

All three approaches have the same time and space complexity but vary in how they solve the subproblems.