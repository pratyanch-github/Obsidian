
`dp[i][j] = lcs starting from ith index of s1 and jth index of s2 `

```
 if(i>=n or j>=m) dp[i][j] = 0
 
 if(s[i]==s[j]) dp[i][j]= dp[i+1][j+1];
 else dp[i][j] = max(dp[i][j+1], dp[i+1][j])  
```
