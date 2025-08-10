Here’s an improved and structured version of your notes for **Kadane's Algorithm**, focusing on both **maximum sum subarray** and **maximum product subarray** problems.

---

### **Kadane's Algorithm Overview**

Kadane’s Algorithm is a **Dynamic Programming** technique that is used to solve problems like:
1. **Maximum Sum Subarray**
2. **Maximum Product Subarray**

In both cases, we are maintaining two key values for each subarray:
- The best subarray ending at the current index.
- The overall maximum result so far.

We can further optimize space by reducing extra storage to just a few variables since each subarray value depends only on the previous one.

---

### **1. Maximum Sum Subarray**

- **Problem Statement**: Find the contiguous subarray with the largest sum.

#### **Dynamic Programming Approach:**

- **dp[i]**: Maximum sum subarray ending at index `i`.
  
![[{72F0BCAE-137E-4062-99C9-ABA01623BE55}.png]]

- **Space Optimization**: Since `dp[i]` only depends on `dp[i-1]`, we can store just one variable (`sum`) to track the maximum sum ending at index `i`.

#### **Code Implementation (C++):**

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int sum = nums[0];  // Maximum sum ending at index i
        int ans = nums[0];  // Overall maximum sum

        for(int i = 1; i < nums.size(); i++) {
            sum = max(nums[i], sum + nums[i]);  // Update sum for the current subarray
            ans = max(ans, sum);  // Update the global maximum
        }

        return ans;
    }
};
```

#### **Key Points**:
- **Time Complexity**: O(n)
- **Space Complexity**: O(1) (after space optimization)
- We only need to store `sum` (the sum ending at the current index) and `ans` (the overall max).

---

### **2. Maximum Product Subarray**

- **Problem Statement**: Find the contiguous subarray with the largest product.

#### **Dynamic Programming Approach:**

Here, the challenge is that the product of subarrays can fluctuate due to negative numbers. To handle this:
- Maintain two variables:
  - **dp1[i]**: Maximum product subarray ending at index `i`.
  - **dp2[i]**: Minimum product subarray ending at index `i` (to handle the negative case).


![[{6178BF54-984A-4502-A061-EB536DEA7CAF}.png]]
#### **Code Implementation (C++):**

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp1(n, -1), dp2(n, -1);  // dp1: max product, dp2: min product
        dp1[0] = nums[0];
        dp2[0] = nums[0];
        
        int ans = nums[0];  // To store the global max product
        
        for(int i = 1; i < n; i++) {
            dp1[i] = max({nums[i], dp1[i-1] * nums[i], dp2[i-1] * nums[i]});
            dp2[i] = min({nums[i], dp1[i-1] * nums[i], dp2[i-1] * nums[i]});
            ans = max(ans, dp1[i]);  // Update the global max product
        }
        
        return ans;
    }
};
```

#### **Key Points**:
- **Time Complexity**: O(n)
- **Space Complexity**: O(n) (can be optimized to O(1) by maintaining just the last values of `dp1` and `dp2`).

#### **Space Optimization**:
Since we only need the previous `dp1[i-1]` and `dp2[i-1]`, we can reduce the space to constant O(1).

---

### **Summary of Kadane's Algorithm**:

1. **Maximum Sum Subarray**:
   - Recurrence: `dp[i] = max(arr[i], dp[i-1] + arr[i])`
   - Track the maximum sum at each step.
   - Time Complexity: O(n), Space Complexity: O(1) (with optimization).

2. **Maximum Product Subarray**:
   - Recurrence:
     - `dp1[i] = max(nums[i], dp1[i-1] * nums[i], dp2[i-1] * nums[i])`
     - `dp2[i] = min(nums[i], dp1[i-1] * nums[i], dp2[i-1] * nums[i])`
   - Track both maximum and minimum products at each step due to negative numbers.
   - Time Complexity: O(n), Space Complexity: O(1) (after optimization).

Both versions follow the same logic of maintaining subarray results ending at each index, but in the case of products, handling negative values is essential, hence the need for tracking both max and min products.

--- 

This structure makes your notes systematic and easy to understand!