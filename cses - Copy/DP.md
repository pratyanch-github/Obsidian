
### 1. Dice Combinations (CSES Problem ID: `1633`)

#### Problem Statement:
You are given an integer `n`. Y  your task is to count the number of ways to write `n` as the sum of numbers `1, 2, ..., 6`. Every number can be used any number of times.

#### Input:
- The only input line has an integer `n` (1 ≤ n ≤ 10^6).

#### Output:
- Print the number of ways modulo `10^9 + 7`.

#### Example:
##### Input 1:
```
3
```

##### Output 1:
```
4
```

##### Explanation:
There are 4 ways to form 3:
1. 1+1+1
2. 1+2
3. 2+1
4. 3

---

### 2. Minimizing Coins (CSES Problem ID: `1634`)

#### Problem Statement:
You are given `n` coins, each with a positive integer value. Your task is to calculate the minimum number of coins needed to construct a sum of money `x`. You can use each coin an unlimited number of times.

#### Input:
- The first input line has two integers `n` and `x`: the number of coins and the desired sum of money (1 ≤ n ≤ 100, 1 ≤ x ≤ 10^6).
- The second line contains `n` integers `c_1, c_2, ..., c_n`: the values of the coins (1 ≤ c_i ≤ 10^6).

#### Output:
- Print one integer: the minimum number of coins. If it is not possible to form the sum, print `-1`.

#### Example:
##### Input 1:
```
3 11
1 5 7
```

##### Output 1:
```
3
```

##### Explanation:
The minimum number of coins required to form 11 is `3` (e.g., 5+5+1).

---

### 3. Coin Combinations I (CSES Problem ID: `1635`)

#### Problem Statement:
Consider a money system consisting of `n` coins. The coins can have any positive integer value. Your task is to calculate the number of distinct ordered ways you can produce a sum of money `x` using the available coins.

#### Input:
- The first input line has two integers `n` and `x`: the number of coins and the desired sum of money (1 ≤ n ≤ 100, 1 ≤ x ≤ 10^6).
- The second line contains `n` integers `c_1, c_2, ..., c_n`: the values of the coins (1 ≤ c_i ≤ 10^6).

#### Output:
- Print the number of ordered ways modulo `10^9 + 7`.

#### Example:
##### Input 1:
```
3 9
2 3 5
```

##### Output 1:
```
8
```

##### Explanation:
There are 8 ordered ways to form 9 using coins with values {2, 3, 5}.

---

### 4. Coin Combinations II (CSES Problem ID: `1636`)

#### Problem Statement:
Consider a money system consisting of `n` coins. The coins can have any positive integer value. Your task is to calculate the number of distinct unordered ways you can produce a sum of money `x` using the available coins.

#### Input:
- The first input line has two integers `n` and `x`: the number of coins and the desired sum of money (1 ≤ n ≤ 100, 1 ≤ x ≤ 10^6).
- The second line contains `n` integers `c_1, c_2, ..., c_n`: the values of the coins (1 ≤ c_i ≤ 10^6).

#### Output:
- Print the number of unordered ways modulo `10^9 + 7`.

#### Example:
##### Input 1:
```
3 9
2 3 5
```

##### Output 1:
```
4
```

##### Explanation:
There are 4 unordered ways to form 9.

---

### 5. Removing Digits (CSES Problem ID: `1637`)

#### Problem Statement:
You are given an integer `n`. On each step, you may subtract one of the digits of `n` from `n`. How many steps are required to make `n` equal to `0`?

#### Input:
- The only input line has an integer `n` (1 ≤ n ≤ 10^6).

#### Output:
- Print one integer: the minimum number of steps.

#### Example:
##### Input 1:
```
27
```

##### Output 1:
```
5
```

##### Explanation:
One possible way to reduce 27 to 0:
27 → 20 → 18 → 10 → 9 → 0 (total 5 steps).

---

### Test Cases

#### 1. Dice Combinations
##### Input:
```
3
```

##### Output:
```
4
```

#### 2. Minimizing Coins
##### Input:
```
3 11
1 5 7
```

##### Output:
```
3
```

#### 3. Coin Combinations I
##### Input:
```
3 9
2 3 5
```

##### Output:
```
8
```

#### 4. Coin Combinations II
##### Input:
```
3 9
2 3 5
```

##### Output:
```
4
```

#### 5. Removing Digits
##### Input:
```
27
```

##### Output:
```
5
```

Here are the **problem statements** and **exact test cases** for the **next 5 CSES Dynamic Programming problems** (problems 6 to 10).

---

### 6. **Grid Paths** (CSES Problem ID: `1638`)

#### Problem Statement:
You are given an `n × n` grid. You want to walk from the upper-left corner to the lower-right corner. On each step, you can go either right or down. Some of the cells are blocked, so you cannot step on them. Count the number of ways you can reach the lower-right corner.

#### Input:
- The first input line has an integer `n` (1 ≤ n ≤ 1000).
- Then there are `n` lines, each containing `n` characters: `.` denotes an empty cell, and `*` denotes a blocked cell.

#### Output:
- Print the number of ways modulo `10^9 + 7`.

#### Example:
##### Input 1:
```
4
....
.*..
...*
....
```

##### Output 1:
```
3
```

##### Explanation:
There are 3 ways to get from the top-left corner to the bottom-right corner, avoiding the blocked cells.

---

### 7. **Book Shop** (CSES Problem ID: `1158`)

#### Problem Statement:
You are in a book shop which sells `n` different books. You know the price and number of pages of each book. You have decided that the total price of the books you buy should be at most `x`. What is the maximum number of pages you can buy?

#### Input:
- The first input line contains two integers `n` and `x`: the number of books and the maximum total price (1 ≤ n ≤ 1000, 1 ≤ x ≤ 10^5).
- The second line contains `n` integers `h_1, h_2, ..., h_n`: the price of each book.
- The third line contains `n` integers `s_1, s_2, ..., s_n`: the number of pages of each book.

#### Output:
- Print one integer: the maximum number of pages.

#### Example:
##### Input 1:
```
4 10
4 8 5 3
5 12 8 1
```

##### Output 1:
```
13
```

##### Explanation:
The maximum number of pages you can buy is 13 (by buying the 1st and 4th books).

---

### 8. **Array Description** (CSES Problem ID: `1746`)

#### Problem Statement:
You have an array of length `n`, and each element is between `1` and `m`, both inclusive. Some of the elements are known, and others are unknown (denoted by `0`). Your task is to count the number of arrays that match this description.

#### Input:
- The first input line has two integers `n` and `m`: the length of the array and the maximum value of each element (1 ≤ n ≤ 100000, 1 ≤ m ≤ 100).
- The second line has `n` integers: the elements of the array. If an element is `0`, it means that the value of that element is unknown.

#### Output:
- Print the number of arrays modulo `10^9 + 7`.

#### Example:
##### Input 1:
```
3 5
2 0 2
```

##### Output 1:
```
3
```

##### Explanation:
There are 3 valid arrays: `[2,1,2]`, `[2,2,2]`, `[2,3,2]`.

---

### 9. **Counting Towers** (CSES Problem ID: `2413`)

#### Problem Statement:
You are given an integer `n`. Your task is to count the number of towers of height `n`. Each tower consists of `n` levels. Each level may be either a 2×1 block or two 1×1 blocks. The tower must be stable, meaning that every level must be supported by a block or blocks on the level directly below it.

#### Input:
- The only input line contains an integer `n` (1 ≤ n ≤ 10^6).

#### Output:
- Print the number of towers modulo `10^9 + 7`.

#### Example:
##### Input 1:
```
3
```

##### Output 1:
```
5
```

---

### 10. **Edit Distance** (CSES Problem ID: `1639`)

#### Problem Statement:
You are given two strings. Your task is to convert the first string into the second string by performing a series of operations. On each operation, you can:
- Insert a character,
- Remove a character, or
- Replace a character.

What is the minimum number of operations needed?

#### Input:
- The first input line has the first string.
- The second input line has the second string. Both strings consist of lowercase letters and have lengths between `1` and `5000`.

#### Output:
- Print one integer: the minimum number of operations required.

#### Example:
##### Input 1:
```
kitten
sitting
```

##### Output 1:
```
3
```

##### Explanation:
To convert "kitten" into "sitting", 3 operations are needed:
1. Replace 'k' with 's'.
2. Insert 'i' after 'k'.
3. Insert 'g' at the end.

---
Here are the **problem statements** and **exact test cases** for the **next 5 CSES Dynamic Programming problems** (problems 11 to 15).

---

### 11. **Money Sums** (CSES Problem ID: `1745`)

#### Problem Statement:
You have `n` coins with certain values. Your task is to calculate all distinct sums that you can form using these coins.

#### Input:
- The first input line contains an integer `n` (1 ≤ n ≤ 100).
- The second line contains `n` integers `x_1, x_2, ..., x_n` (1 ≤ x_i ≤ 1000): the value of each coin.

#### Output:
- Print an integer `k`: the number of distinct sums.
- After that, print all distinct sums in increasing order.

#### Example:
##### Input 1:
```
3
2 3 5
```

##### Output 1:
```
7
2 3 5 7 8 10
```

---

### 12. **Removal Game** (CSES Problem ID: `1097`)

#### Problem Statement:
Two players play a game where they remove numbers from a list. Both players know the entire list of numbers and play optimally. The players take turns removing numbers from either end of the list, and the score of a player is the sum of the numbers they have removed. What is the maximum possible score the first player can achieve?

#### Input:
- The first input line contains an integer `n` (1 ≤ n ≤ 5000): the number of elements in the list.
- The second line contains `n` integers `x_1, x_2, ..., x_n` (1 ≤ x_i ≤ 10^9): the numbers in the list.

#### Output:
- Print the maximum possible score the first player can achieve.

#### Example:
##### Input 1:
```
4
4 5 1 3
```

##### Output 1:
```
8
```

##### Explanation:
The first player can achieve a score of 8 by taking `4` first, and then `3`, leaving the second player with a maximum possible score of `5 + 1 = 6`.

---

### 13. **Two Sets II** (CSES Problem ID: `1093`)

#### Problem Statement:
Your task is to divide the numbers `1, 2, ..., n` into two sets of equal sum. If there are multiple ways to do this, find the number of such ways.

#### Input:
- The only input line has an integer `n` (1 ≤ n ≤ 500).

#### Output:
- Print one integer: the number of ways to divide the set into two sets of equal sum modulo `10^9 + 7`. If no solution exists, print `0`.

#### Example:
##### Input 1:
```
7
```

##### Output 1:
```
4
```

##### Explanation:
There are four ways to divide the set `{1, 2, 3, 4, 5, 6, 7}` into two sets of equal sum.

---

### 14. **Increasing Subsequence** (CSES Problem ID: `1145`)

#### Problem Statement:
You are given an array of `n` integers, and your task is to find the length of the longest increasing subsequence in the array.

#### Input:
- The first input line contains an integer `n` (1 ≤ n ≤ 2 × 10^5): the size of the array.
- The second line contains `n` integers `x_1, x_2, ..., x_n` (1 ≤ x_i ≤ 10^9): the elements of the array.

#### Output:
- Print the length of the longest increasing subsequence.

#### Example:
##### Input 1:
```
8
7 3 5 3 6 2 9 8
```

##### Output 1:
```
4
```

##### Explanation:
One longest increasing subsequence is `[3, 5, 6, 9]`.

---

### 15. **Projects** (CSES Problem ID: `1140`)

#### Problem Statement:
You are given `n` projects. Each project has a starting day, an ending day, and a reward. You can only work on one project at a time. What is the maximum reward you can collect?

#### Input:
- The first input line contains an integer `n` (1 ≤ n ≤ 2 × 10^5): the number of projects.
- After this, there are `n` lines, each containing three integers `a_i, b_i, p_i`: the starting day, ending day, and reward for a project.

#### Output:
- Print one integer: the maximum reward you can collect.

#### Example:
##### Input 1:
```
3
1 3 10
2 5 20
3 6 30
```

##### Output 1:
```
40
```

##### Explanation:
You can choose the first and third projects to collect a reward of 40.

---

