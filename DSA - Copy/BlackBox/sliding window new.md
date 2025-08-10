
Here is the reorganized and expanded version of the sliding window template notes:

# Sliding Window Template

## General Sliding Window Approach

```
int l = 0;
for (int r = 0; r < n; r++) {
    // Add arr[r] to the window and update window properties
    
    // If the window is valid:
    {
        // Update the answer
    }
    else {
        // Remove arr[l] from the window and update window properties
        l++;
    }
}
```

If we don't want to write the "update answer" statement inside the loop, we can do it at the end:

```
int l = 0;
for (int r = 0; r < n; r++) {
    // Add arr[r] to the window and update window properties
    
    // Remove arr[l] from the window and update window properties
    while (window is not valid) {
        l++;
    }
    
    // Window is now valid, update the answer
}
```

## Types of Sliding Window Problems

1. **Constant-Size Window Problems**
   - The window size remains fixed throughout the process.
   - Example: ![[Pasted image 20240518133926.png]]

2. **Longest Subarray/Substring with a Condition**
   - Brute Force Approach: O(n^2)
   - Optimized Approaches:
     - O(2n) Approach: 
       - Initialize `head = 0`, `tail = 0`
       - Expand the window by incrementing `head` continuously
       - If the window becomes invalid, shrink the window by incrementing `tail` until it becomes valid again
       - Update the answer and increment `head`
       - Example: Longest subarray with sum less than or equal to `k`
     - O(n) Approach:
       - Initialize `head = 0`, `tail = 0`
       - Expand the window by incrementing `head` continuously
       - If the window becomes invalid, don't shrink it, just increment `tail`
       - Update the answer and increment `head`
       - This approach is only applicable if we just need to return the size of the window, not the actual window.
       - Example: ![[Pasted image 20240518141141.png]]

3. **Sliding Window with "At Least" Problems**
   ```
   for (int r = 0; r < n; r++) {
        // Add arr[r] to the window and update window properties
        
        // While the window is valid:
        {
            // Update the answer
            ans += n - r;
            
            // Remove arr[l] from the window and update window properties
        }
   }
   ```
   Example: Number of subarrays with at least `k` distinct elements.

## Variations and Examples

1. **Longest Subarray/Substring with at Most `K` Zeros**
   Example: [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)
   ```cpp
   int longestOnes(vector<int>& A, int K) {
       int i = 0, j;
       for (j = 0; j < A.size(); ++j) {
           if (A[j] == 0) K--;
           if (K < 0 && A[i++] == 0) K++;
       }
       return j - i;
   }
   ```

2. **Sliding Window with "At Least" Problems**
   Example: Number of subarrays with at least `k` distinct elements.
   ```
   for (int r = 0; r < n; r++) {
        // Add arr[r] to the window and update window properties
        
        // While the window is valid:
        {
            // Update the answer
            ans += n - r;
            
            // Remove arr[l] from the window and update window properties
        }
   }
   ```

Remember, the key to solving sliding window problems is to maintain a valid window and update the answer accordingly. The specific implementation details may vary depending on the problem constraints and requirements.



Got it, here are the explanations for the 10 hard LeetCode sliding window problems using the provided templates, implemented in C++:

1. **Longest Substring Without Repeating Characters**
   - Explanation:
     
     
     ```cpp
class Solution {
     public:
         int lengthOfLongestSubstring(string s) {
             // Initialize the window
             unordered_set<char> window;
             int left = 0, right = 0;
             int maxLen = 0;
             
             while (right < s.length()) {
                 // If the current character is not in the window, add it
                 if (window.find(s[right]) == window.end()) {
                     window.insert(s[right]);
                     maxLen = max(maxLen, right - left + 1);
                     right++;
                 }
                 // If the current character is in the window, remove characters from the left
                 else {
                     window.erase(s[left]);
                     left++;
                 }
             }
             
             return maxLen;
         }
     };
     
```
     
     - Time complexity: O(n), where n is the length of the input string.
     - Space complexity: O(min(m, n)), where m is the size of the character set (since we use a HashSet to store the unique characters in the current window).

2. **Minimum Window Substring**
   - Explanation:
     
     
     ```cpp
class Solution {
     public:
         string minWindow(string s, string t) {
             // Initialize the window and the target character count
             unordered_map<char, int> window, target;
             for (char c : t) {
                 target[c]++;
             }
             
             // Initialize the pointers and the minimum window length
             int left = 0, right = 0;
             int minLen = INT_MAX, minStart = 0;
             int missing = t.length();
             
             while (right < s.length()) {
                 // If the current character is in the target, decrement the missing count
                 if (target.find(s[right]) != target.end()) {
                     window[s[right]]++;
                     if (window[s[right]] <= target[s[right]]) {
                         missing--;
                     }
                 }
                 
                 // If all characters in the target are found, try to shrink the window
                 while (missing == 0) {
                     // Update the minimum window length and start index
                     if (right - left + 1 < minLen) {
                         minLen = right - left + 1;
                         minStart = left;
                     }
                     
                     // If the character at the left pointer is in the target, increment the missing count
                     if (target.find(s[left]) != target.end()) {
                         window[s[left]]--;
                         if (window[s[left]] < target[s[left]]) {
                             missing++;
                         }
                     }
                     
                     left++;
                 }
                 
                 right++;
             }
             
             return minLen == INT_MAX ? "" : s.substr(minStart, minLen);
         }
     };
     
```
     
     - Time complexity: O(n), where n is the length of the input string.
     - Space complexity: O(m + n), where m is the length of the target string `t`, and n is the length of the input string `s`.

3. **Sliding Window Maximum**
   - Explanation:
     
     
     ```cpp
class Solution {
     public:
         vector<int> maxSlidingWindow(vector<int>& nums, int k) {
             // Initialize the deque and the result list
             deque<int> dq;
             vector<int> result;
             
             for (int i = 0; i < nums.size(); i++) {
                 // Remove any elements from the deque that are smaller than the current element
                 while (!dq.empty() && nums[dq.back()] < nums[i]) {
                     dq.pop_back();
                 }
                 
                 // Add the current index to the deque
                 dq.push_back(i);
                 
                 // If the leftmost element in the deque is out of the current window, remove it
                 if (dq.front() == i - k) {
                     dq.pop_front();
                 }
                 
                 // If the current index is >= k-1, add the maximum element to the result
                 if (i >= k - 1) {
                     result.push_back(nums[dq.front()]);
                 }
             }
             
             return result;
         }
     };
     
```
     
     - Time complexity: O(n), where n is the length of the input array.
     - Space complexity: O(k), where k is the size of the sliding window.

4. **Subarrays with K Different Integers**
   - Explanation:
     
     
     ```cpp
class Solution {
     public:
         int subarraysWithKDistinct(vector<int>& nums, int k) {
             return atMost(nums, k) - atMost(nums, k - 1);
         }
         
     private:
         int atMost(vector<int>& nums, int k) {
             // Count the number of subarrays with at most k distinct integers
             int count = 0;
             int left = 0, right = 0;
             unordered_map<int, int> window;
             
             while (right < nums.size()) {
                 // Expand the window by adding the current element
                 window[nums[right]]++;
                 
                 // Shrink the window until the number of distinct elements is <= k
                 while (window.size() > k) {
                     window[nums[left]]--;
                     if (window[nums[left]] == 0) {
                         window.erase(nums[left]);
                     }
                     left++;
                 }
                 
                 // The number of subarrays is right - left + 1
                 count += right - left + 1;
                 right++;
             }
             
             return count;
         }
     };
     
```
     
     - Time complexity: O(n), where n is the length of the input array.
     - Space complexity: O(k), where k is the number of distinct integers in the array.

5. **Longest Repeating Character Replacement**
   - Explanation:
     
     
     ```cpp
class Solution {
     public:
         int longestRepeatingCharacterReplacement(string s, int k) {
             // Initialize the window and the maximum count of any character
             unordered_map<char, int> window;
             int maxCount = 0;
             int maxLen = 0;
             
             int left = 0, right = 0;
             
             while (right < s.length()) {
                 // Expand the window by adding the current character
                 window[s[right]]++;
                 maxCount = max(maxCount, window[s[right]]);
                 
                 // If the window size minus the maximum count is greater than k,
                 // we need to shrink the window
                 while (right - left + 1 - maxCount > k) {
                     window[s[left]]--;
                     if (window[s[left]] == 0) {
                         window.erase(s[left]);
                     }
                     left++;
                     maxCount = *max_element(window.begin(), window.end(), [](auto& a, auto& b) {
                         return a.second < b.second;
                     })->second;
                 }
                 
                 // Update the maximum length
                 maxLen = max(maxLen, right - left + 1);
                 right++;
             }
             
             return maxLen;
         }
     };
     
```
     
     - Time complexity: O(n), where n is the length of the input string.
     - Space complexity: O(1), since the size of the character set is constant (26 for uppercase English letters).

6. **Substring with Concatenation of All Words**
   - Explanation:
     
     
     ```cpp
class Solution {
     public:
         vector<int> findSubstring(string s, vector<string>& words) {
             if (s.empty() || words.empty()) {
                 return {};
             }
             
             // Initialize the word length, word count, and result list
             int wordLen = words[0].length();
             int wordCount = words.size();
             vector<int> result;
             
             // Count the words in the words list
             unordered_map<string, int> wordFreq;
             for (const string& word : words) {
                 wordFreq[word]++;
             }
             
             // Iterate through the string s
             for (int i = 0; i <= s.length() - wordLen * wordCount; i++) {
                 // Get the current window of words
                 unordered_map<string, int> window;
                 for (int j = i; j < i + wordLen * wordCount; j += wordLen) {
                     string word = s.substr(j, wordLen);
                     if (wordFreq.find(word) == wordFreq.end()) {
                         break;
                     }
                     window[word]++;
                     if (window[word] > wordFreq[word]) {
                         break;
                     }
                 }
                 
                 // If the current window is a valid concatenation, add the starting index to the result
                 if (window == wordFreq) {
                     result.push_back(i);
                 }
             }
             
             return result;
         }
     };
     
```
     
     - Time complexity: O(n * m), where n is the length of the input string `s`, and m is the length of the `words` list.
     - Space complexity: O(m), where m is the length of the `words` list.

7. **Minimum Size Subarray Sum**
   - Explanation:
     
     
     ```cpp
class Solution {
     public:
         int minSubArrayLen(int target, vector<int>& nums) {
             int left = 0, right = 0;
             int minSize = INT_MAX;
             int currSum = 0;
             
             while (right < nums.size()) {
                 // Expand the window by adding the current element
                 currSum += nums[right];
                 
                 // Shrink the window until the sum is less than the target
                 while (currSum >= target) {
                     // Update the minimum size subarray
                     minSize = min(minSize, right - left + 1);
                     
                     // Remove the leftmost element from the window
                     currSum -= nums[left];
                     left++;
                 }
                 
                 right++;
             }
             
             return minSize == INT_MAX ? 0 : minSize;
         }
     };
     
```
     
     - Time complexity: O(n), where n is the length of the input array.
     - Space complexity: O(1), since we only use a constant amount of extra space.

8. **Max Consecutive Ones III**
   - Explanation:
     
     
     ```cpp
class Solution {
     public:
         int longestOnes(vector<int>& nums, int k) {
             int left = 0, right = 0;
             int maxLen = 0;
             int zeroCount = 0;
             
             while (right < nums.size()) {
                 // If the current element is 0, increment the zero count
                 if (nums[right] == 0) {
                     zeroCount++;
                 }
                 
                 // If the zero count is greater than k, shrink the window
                 while (zeroCount > k) {
                     if (nums[left] == 0) {
                         zeroCount--;
                     }
                     left++;
                 }
                 
                 // Update the maximum length
                 maxLen = max(maxLen, right - left + 1);
                 right++;
             }
             
             return maxLen;
         }
     };
     
```
     
     - Time complexity: O(n), where n is the length of the input array.
     - Space complexity: O(1), since we only use a constant amount of extra space.

9. **Fruit Into Baskets**
   - Explanation:
     
     
     ```cpp
class Solution {
     public:
         int totalFruit(vector<int>& fruits) {
             int left = 0, right = 0;
             int maxLen = 0;
             unordered_map<int, int> window;
             
             while (right < fruits.size()) {
                 // Add the current fruit to the dictionary
                 window[fruits[right]]++;
                 
                 // If the number of distinct fruit types is greater than 2, shrink the window
                 while (window.size
```