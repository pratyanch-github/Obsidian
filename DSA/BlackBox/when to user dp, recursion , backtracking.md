Let’s break down these concepts with clarity and examples to build your intuition. Think of them as tools in a toolbox—each solves specific types of problems.

---

### **1. Recursion**
**What**: A function calls itself to solve smaller instances of the same problem.  
**When to Use**:  
- Problems with **self-similar structure** (e.g., factorial, Fibonacci, tree traversals).  
- When the problem can be divided into smaller, identical subproblems.  

**Example**:  
```python
def factorial(n):
    if n == 0:
        return 1
    return n * factorial(n-1)
```

**Mindset**:  
- **Base Case**: Define the simplest case (e.g., `n=0` for factorial).  
- **Recursive Step**: Reduce the problem size (`n-1`).  

**Limitations**:  
- Can be inefficient for overlapping subproblems (e.g., Fibonacci recalculates `fib(3)` multiple times).  
- Risk of stack overflow for deep recursion.  

---

### **2. Backtracking**
**What**: A refined form of recursion to **explore all possible solutions** by building candidates incrementally and abandoning ("backtracking") invalid paths.  
**When to Use**:  
- **Combinatorial problems** (permutations, subsets, N-Queens).  
- **Decision-making with constraints** (Sudoku, maze solving).  

**Example (Generate Permutations)**:  
```python
def permute(nums):
    res = []
    def backtrack(path, remaining):
        if not remaining:
            res.append(path.copy())
            return
        for num in remaining:
            path.append(num)
            backtrack(path, [x for x in remaining if x != num])  # Remove chosen num
            path.pop()  # Backtrack
    backtrack([], nums)
    return res
```

**Mindset**:  
- **Decision Tree**: Visualize choices as branches in a tree.  
- **Pruning**: Skip paths that violate constraints early (e.g., invalid Sudoku placements).  
- **Undo Choices**: Reset state after recursion to explore other branches.  

**Key Insight**:  
Backtracking is **DFS with state management** (adding/removing choices).  

---

### **3. Depth-First Search (DFS)**
**What**: An algorithm to **traverse trees/graphs** by exploring as far as possible along a branch before backtracking.  
**When to Use**:  
- **Pathfinding** (mazes, connectivity checks).  
- **Topological sorting**, cycle detection.  

**Example (Tree Traversal)**:  
```python
class Node:
    def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

def dfs(root):
    if not root:
        return
    print(root.val)  # Pre-order traversal
    dfs(root.left)
    dfs(root.right)
```

**Relation to Backtracking**:  
- Backtracking uses DFS to explore paths but adds **state modification/rollback**.  

---

### **4. Dynamic Programming (DP)**
**What**: Optimizes recursive solutions by **storing results of subproblems** to avoid redundant calculations.  
**When to Use**:  
- **Overlapping Subproblems**: The same subproblem is solved multiple times (e.g., Fibonacci).  
- **Optimal Substructure**: The optimal solution can be built from optimal solutions to subproblems (e.g., shortest path).  

**Example (Fibonacci with Memoization)**:  
```python
memo = {}
def fib(n):
    if n <= 1:
        return n
    if n in memo:
        return memo[n]
    memo[n] = fib(n-1) + fib(n-2)
    return memo[n]
```

**Mindset**:  
- **Memoization (Top-Down)**: Cache results of subproblems (like recursion with a memo table).  
- **Tabulation (Bottom-Up)**: Build solutions iteratively from smallest subproblems (e.g., DP tables).  

**Example (Dice Problem with DP)**:  
To count ways to reach sum `n` using dice (order matters):  
```python
def count_permutations(n):
    dp = [0] * (n + 1)
    dp[0] = 1  # Base case: 1 way to sum 0
    for i in range(1, n + 1):
        for dice in range(1, 7):
            if dice <= i:
                dp[i] += dp[i - dice]
    return dp[n]
```

---

### **5. Printing Solutions with DP**
**What**: Reconstruct the sequence of decisions that led to the optimal solution.  
**How**: Track choices during DP table construction.  

**Example (Coin Change)**:  
Given coins `[1, 2, 5]` and target `n=6`, find the coins used:  
```python
def coin_change(n):
    dp = [float('inf')] * (n + 1)
    dp[0] = 0
    prev_coin = [-1] * (n + 1)  # Track last coin used

    for i in range(1, n + 1):
        for coin in [1, 2, 5]:
            if coin <= i and dp[i - coin] + 1 < dp[i]:
                dp[i] = dp[i - coin] + 1
                prev_coin[i] = coin  # Track the coin

    # Reconstruct the solution
    path = []
    current = n
    while current > 0:
        coin = prev_coin[current]
        path.append(coin)
        current -= coin
    return path
```

**Output**: `[5, 1]` (coins summing to 6).  

---

### **When to Use Which?**
| **Technique**      | **Use Case**                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| **Recursion**       | Simple problems without overlapping subproblems (e.g., tree traversals).    |
| **Backtracking**    | Exhaustive search with constraints (e.g., permutations, puzzles).           |
| **DFS**             | Graph/tree traversal, pathfinding.                                         |
| **Dynamic Programming** | Optimization problems with overlapping subproblems (e.g., Fibonacci, shortest path). |
| **DP + Printing**   | Reconstructing the optimal path after solving with DP.                      |

---

### **Decision Flowchart**  
1. **Need all possible solutions?** → **Backtracking**.  
2. **Optimal solution with overlapping subproblems?** → **DP**.  
3. **Traversing a graph/tree?** → **DFS/BFS**.  
4. **Simple recursive structure?** → **Recursion**.  

---

### **Key Takeaways**  
- **Recursion**: The foundation. Use for divide-and-conquer problems.  
- **Backtracking**: Use for constraint-based combinatorial search.  
- **DFS**: A traversal strategy (often used in backtracking).  
- **DP**: Optimize recursion by storing subproblem results.  

Practice these concepts with problems like **Fibonacci** (recursion → DP), **N-Queens** (backtracking), and **Coin Change** (DP + path reconstruction). Over time, you’ll intuitively choose the right tool! 🚀