Template - 

![[Pasted image 20240517213555.png]]

Sliding window has 4 types of problems - 

1. constant window problems 
     ![[Pasted image 20240518133926.png]]


2. Longest Subarray/Substring - with some condition
      - Brute Force Approach 
      
      - O(2n) Approach : Ex. longest subarray with sum less than or equal to k 
      
	      -  Initially head =0 , tail=0 
	      -  we expand the head continuously, using While
	          - after expanding one step - as result window can be valid/ nonvalid
	          - shrink till window(tail++) till window becomes valid, using While
	          - update answer and do head++
	     ![[Pasted image 20240518135527.png]]
	          
	          
	          
     - O(n) Approach : 
         This approach is only applicable if we have to just return size of window, now the actual window.
          
          -  Initially head =0 , tail=0 
	      -  we expand the head continuously, using While
	          - after expanding one step - as result window can be valid/ nonvalid
	          - if window is invalid just do tail++, (don't shrink to make the window becomes valid) i.e we don't want to shrink beyond current max length.
	             Because earlier we were shrinking it till window becomes valid and sometimes we shrink it below the current maxlength so we have to expand it again till maxlength and ahed
	          - update answer and do head++
	     
	      ![[Pasted image 20240518141141.png]]
	            
	       Note : in this O(n) approach then the outer while loop terminates then the (tail) will still present at index (head - maxlen). So we can return maxlen or ans = head-tail .    

			[ 0 0 0 0 0 0 0 0 1 1 1 1 0 0 0 0 ] 
                              tail            head
     
         example - [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)
          ```
             int longestOnes(vector<int>& A, int K) {
			        int i = 0, j;
			        for (j = 0; j < A.size(); ++j) {
			            if (A[j] == 0) K--;
			            if (K < 0 && A[i++] == 0) K++;
			        }
			        return j - i;
			    }
            ```
 