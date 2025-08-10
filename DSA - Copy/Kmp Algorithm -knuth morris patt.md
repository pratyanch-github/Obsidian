1. It is a string matching algorithm. Like we can find a pattern(sol string) in a big string. If pattern is of length m and big string of n then time complexity of bruteforce is mxn.
   ![[Pasted image 20240323141619.png]]
2. It uses the fact that if we once started matching the pattern then for next pattern onwards we only need to check pattern after the longest prefix = longest suffix .
   ![[Pasted image 20240323141703.png]]
3. 