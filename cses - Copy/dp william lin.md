
# 1. dice combination 
![[Pasted image 20250517190027.png]]

# 2. minimizing coins
![[Pasted image 20250517190325.png]]

# 3.  Coin combination 1
 ![[Pasted image 20250517191004.png]]
# 4. Coin change 2
![[Pasted image 20250517235442.png]]

# 7 Book Shop (knapsac)- 
normally we use two parameters "dp(i)(x) = max( dp(i-1)(x) , dp(i-1)(x-price(i)) )" but here we are using just dp(x) , because this is space optimized solution, we are able to space optimize because dpi depends only on dpi-1 so we can just use single array instead of grid. 
![[Pasted image 20250521083405.png]]
# **Knapsack Problem: From 2D to 1D DP (Beginner-Friendly Notes)**  

## **1. Problem Statement (Book Shop Problem)**
- **Given:**  
  - `n` books, each with a **price** `h[i]` and **pages** `s[i]`.  
  - A **maximum budget** `x`.  
- **Goal:**  
  - Buy books (each at most once) such that total **price ≤ x** and **pages maximized**.  

---

## **2. Simple Approach (2D DP)**
### **Intuition**
- We need to track **two things**:
  1. **How many books we have considered so far (`i`)**  
  2. **How much money we have spent (`j`)**  
- `dp[i][j]` = max pages using first `i` books with budget `j`.

### **DP Definition**
- `dp[i][j]` = Maximum pages achievable by:
  - **Not taking the i-th book** → `dp[i-1][j]`  
  - **Taking the i-th book (if possible)** → `dp[i-1][j - h[i]] + s[i]`  

### **Pseudocode (2D DP)**
```cpp
int dp[n+1][x+1] = {0}; // Initialize all to 0

for(int i = 1; i <= n; i++) {
    for(int j = 0; j <= x; j++) {
        dp[i][j] = dp[i-1][j]; // Don't take the book
        if(j >= h[i-1]) {
            dp[i][j] = max(dp[i][j], dp[i-1][j - h[i-1]] + s[i-1]); // Take the book
        }
    }
}
cout << dp[n][x];
```

### **Key Observations**
✅ **Easy to understand** (explicitly tracks which books are used).  
❌ **Uses O(n×x) space** (not efficient for large `x`).  

---

## **3. Space Optimization (1D DP)**
### **Why Can We Optimize?**
- **Only the previous row (`i-1`) is needed** to compute the current row (`i`).  
- Instead of storing full `dp[i][j]`, we can **overwrite the same array** if we iterate **backwards**.  

### **Why Backward Iteration?**
- If we iterate **forwards**, `dp[j - h[i]]` may already include the current book (**incorrectly using it twice**).  
- **Backward iteration ensures** `dp[j - h[i]]` is from the **previous state (`i-1`)**.  

### **Pseudocode (1D DP)**
```cpp
int dp[x+1] = {0}; // Initialize all to 0

for(int i = 0; i < n; i++) {
    for(int j = x; j >= h[i]; j--) { // Iterate backwards!
        dp[j] = max(dp[j], dp[j - h[i]] + s[i]);
    }
}
cout << dp[x];
```

### **Key Observations**
✅ **Uses only O(x) space** (much more efficient).  
✅ **Same logic as 2D, but optimized**.  
⚠ **Must iterate `j` backwards to avoid overcounting**.  

---

## **4. Summary Table (2D vs 1D DP)**
| Feature          | 2D DP (`dp[i][j]`) | 1D DP (`dp[j]`) |
|------------------|-------------------|----------------|
| **Space**        | O(n×x)            | O(x)           |
| **Iteration**    | Normal (`j=0` to `x`) | Backwards (`j=x` to `h[i]`) |
| **Ease of Understanding** | Easier (explicit states) | Trickier (requires backward loop) |
| **Best For**     | Learning DP        | Competitive Programming |

---

## **5. Final Notes**
1. **Start with 2D DP** to understand the transitions.  
2. **Optimize to 1D** once comfortable with the logic.  
3. **Always iterate backwards in 1D** to prevent duplicate usage.  
4. **Time Complexity** for both approaches: **O(n×x)**.  

### **When to Use Which?**
- **Use 2D DP** when learning or debugging.  
- **Use 1D DP** in contests for better space efficiency.  

---

### Understanding Why We Iterate Backwards in the Knapsack DP

### The Core Problem

In the 0/1 Knapsack (which this book shop problem is), each item (book) can be used **at most once**. If we iterate forwards (from `h[i]` to `x`), we might accidentally use the same book multiple times.


### 1. Forward Iteration (Wrong Approach)
If we do:
```cpp
for(int j = h[i]; j <= x; j++) {
    dp[j] = max(dp[j], dp[j - h[i]] + s[i]);
}
```

**What happens:**
- When we update `dp[j]`, we use `dp[j - h[i]]`
- But `dp[j - h[i]]` might have already included the current book
- This leads to using the same book multiple times

### 2. Backward Iteration (Correct Approach)
```cpp
for(int j = x; j >= h[i]; j--) {
    dp[j] = max(dp[j], dp[j - h[i]] + s[i]);
}
```

**Why it works:**
- We process larger budgets first
- When we get to smaller budgets, we haven't updated them yet with the current book
- This ensures we don't "see" the current book in `dp[j - h[i]]`

## Concrete Example

Let's say:
- Budget `x` = 5
- Book: price = 2, pages = 3

### Forward Iteration (Wrong):

Initial dp: [0, 0, 0, 0, 0, 0]

Processing j=2 to 5:
1. j=2: dp[2] = max(0, dp[0]+3) = 3 → dp: [0, 0, 3, 0, 0, 0]
2. j=3: dp[3] = max(0, dp[1]+3) = 3 → dp: [0, 0, 3, 3, 0, 0]
3. j=4: dp[4] = max(0, dp[2]+3) = 6 → dp: [0, 0, 3, 3, 6, 0]
4. j=5: dp[5] = max(0, dp[3]+3) = 6 → dp: [0, 0, 3, 3, 6, 6]

**Problem:** We used the same book multiple times (see how dp[4] = 6 means we used the book twice)

### Backward Iteration (Correct):

Initial dp: [0, 0, 0, 0, 0, 0]

Processing j=5 down to 2:
1. j=5: dp[5] = max(0, dp[3]+3) = 3 → dp: [0, 0, 0, 0, 0, 3]
2. j=4: dp[4] = max(0, dp[2]+3) = 3 → dp: [0, 0, 0, 0, 3, 3]
3. j=3: dp[3] = max(0, dp[1]+3) = 3 → dp: [0, 0, 0, 3, 3, 3]
4. j=2: dp[2] = max(0, dp[0]+3) = 3 → dp: [0, 0, 3, 3, 3, 3]

**Correct:** Each book is used at most once. Max pages with budget 5 is 3 (only one book used)

## Key Insight

The backward iteration ensures that when we consider using a book for a particular budget `j`, the smaller budget `j - h[i]` we check **hasn't** already been updated with this book yet. This guarantees each book is only considered once.

This is why the order matters so much in the 0/1 Knapsack problem's DP solution! 

---

## **6. Conclusion**
- **2D DP → Easy to understand** but uses more space.  
- **1D DP → Space optimized** but requires careful backward iteration.  
- **Backward loop prevents overcounting** (ensures each book is used at most once).  

**Keep this as a cheat sheet!** 🚀