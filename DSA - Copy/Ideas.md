1. Running Mean Median Mode - it is a stl question , and can also be solved with segment trees but segTrees is Overkill for it.
   
   Maintain a map<int, int>: (ele,freq) for storing frequencies and a multiset<pair<int,int>> for (freq,ele) to maintain order , so the last element of multiset has heighest frequency .
   
   Example-
   https://leetcode.com/problems/most-frequent-ids/
2. Merge Intervals  - (l1,r1), (l2,r2) - intersection is {max(l1,l2) , min(r1,r2)} and if r1>l2 or l1>r2 , the intersection is empty. (hint visualize this )
   
3. Eculidian's  Gcd - Says that Gcd(a,b) =x with b>a is equal to Gcd(a,b%a) =x. 
   Hint: if b-a is also divisible by x, i.e remove all the a's from b (i.e b%a ) and this remainder will also have. 
   
4. 