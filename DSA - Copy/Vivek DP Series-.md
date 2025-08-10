
1. ![[WhatsApp Image 2024-03-14 at 10.31.59_713ab532.jpg]]
2. Dp is just Strategic Backtracking + Caching 
3. So for Backtracking we have to be good at recursion -
   and follow the Level, Choice, Check, Move Framework.
   ![[Pasted image 20240314102253.png]]
4.  

Remember a question can be solved with multiple forms. I depends on how we formulate the state.

--------------------------------------------------------
**Pattern 1** - Take Not Take Form - 
   generally used to generate subsets or subsequence i.e build the answer digit by digit

Given an array of length n, and we are currently at index i and we have to find best solution from index [i........n-1].
State :  
       1. DP[i]= best solution from [i......n-1].
       2. DP[i,someResultFromPreviousChoices] = best solution from [i......n-1] and for at level i we can choose a choice based on someResultFromPreviousChoices. 

Choices :  if we are at index i we can take ith element or don't take ith element.

Time Complexity = #States*(1+ cost of transition at each State)
      cost of transition at each state = generally #Transitions
      #States = product of possible values of each parameter in function 
Template - 
```
      Function rec(i, sumtaken):
    // Pruning: 
    If sumtaken > x:
        Return 0

    // Base case:
    If i == n:
        // If the current sum equals the target sum, we found a valid combination
        If sumtaken == x:
            Return 1
        Else:
            Return 0

    // Cache check: 
    If dp[i][sumtaken] != -1:
        Return dp[i][sumtaken]

    // Transitions: 
    ans = 0
    If rec(i + 1, sumtaken + arr[i]) == 1:
        ans = 1
    If rec(i + 1, sumtaken) == 1:
        ans = 1

    // Save and return the result in the cache
    dp[i][sumtaken] = ans
    Return ans

```
      
Classical Examples- 
1. Subset Generation Problems
2. Creating amount x form [coin1, coin2 ,coin3] , conditioned on quantity number of each coin available(limited supply of coins), no condition(infinite supply of coins)

Non Classical Examples-
1. 


-------------------------------------------------------

**Pattern 2** - Ending/Starting Form

Given an array of length n.  we need to find best answer to the problem ending at index i.
         [ 0,0,0,0,0,0 ] 0,0,0,0,0     
 Here we travel level by level i.e i=0 then i=1, ...... i=n-1, and when we are ith level we calculate DP[i] and use that DP[i] for calculating next states i.e DP[i+something].  

Questions We can ask to ourselves: 
     1.Ending form:  best answer we can get in [0...........i], i will use that to find answer of DP[i+something]
     2.Starting form:  i have calculated answer of [0......i] , you find the answer from [i+1........n].

 ==NOTE==- after creating the DP array we have to traverse it at the end, to find the best solution.   
     
State :  
       1. DP[i]= considered range is [0...........i], best solution ending at index i .

Choices : here for calculation DP[i], 
        we can use best of (DP[i-1],DP[i-2].............DP[0]).

Time Complexity: #States*(1+ #Transitions )

Classical Examples- 
1. Longest Increasing Subsequence. [Form2](https://leetcode.com/problems/longest-increasing-subsequence/submissions/961582151) (can also be done using [Form1](https://leetcode.com/problems/longest-increasing-subsequence/submissions/1019191589))
2. 

Non Classical Examples-
1. 

--------------------------------------------------
**Pattern 6** - Knapsack DP

In this, the choices array can be given mostly , but sometimes we have to assume.


Classical Examples- 
1. [Dice Combinations](https://cses.fi/problemset/task/1633/) - 
     ![[Pasted image 20240515122805.png]]
2. [Minimizing Coins](https://cses.fi/problemset/task/1634) - 
      ![[Pasted image 20240515122739.png]]
3.  Removing digits cses -
      ![[Pasted image 20240515153245.png]]
  4. 
4. Grid Paths cses -
      ![[Pasted image 20240515153944.png]]
5. Array Description - 
     ![[Pasted image 20240515160853.png]]
     ![[Pasted image 20240515160937.png]]
     ![[Pasted image 20240515161221.png]]
6. 



-------------------------------------------

**Pattern 7** - Partitioning DP (similar to staring form)

Given a string or array , and we have to partition based on some condition, and we want to get the min/max number of partitions we can do satistying the condition.

State :  
       1. DP[i]= considered range is [0...........i], best solution ending at index i .


Classical Examples- 
1. 
2. 

Non Classical Examples-
1. [Minimum Substring Partition of Equal Character Frequency](https://leetcode.com/problems/minimum-substring-partition-of-equal-character-frequency/)
2. [Partition Array for Maximum Sum](https://leetcode.com/problems/partition-array-for-maximum-sum/)
