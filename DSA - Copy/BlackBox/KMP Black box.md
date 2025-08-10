
we have 2 strings,  a text and we have a pattern , we have to 
1. find if pattern is present in text or not
2. find the position of pattern in text 

Brute force string searching algorithm 

![[{92484E8F-7CB1-44AA-A22F-43CF6C351531} 1.png]]

![[{C204448E-9595-4652-B2CD-A5F6A0927BDB}.png]]

we use i pointer for moving in text and j in patter, 
![[Pasted image 20241014144822.png]]

![[{175571F0-71B5-44A1-B972-11784CDC47D1}.png]]![[Pasted image 20241014144901.png]]

![[Pasted image 20241014144912.png]]

![[Pasted image 20241014144934.png]] 

![[WhatsApp Image 2024-10-14 at 14.55.55_24099ff2.jpg]]

KMP

The **KMP (Knuth-Morris-Pratt)** algorithm is an efficient string-searching algorithm that helps find occurrences of a pattern within a text. The key point that makes the KMP algorithm efficient is its use of a **partial match (prefix) table**, also known as the **LPS (Longest Prefix Suffix) array**.

### Key Points:

1. **LPS Array (Longest Prefix Suffix)**:
   - The LPS array stores the lengths of the longest proper prefix of the pattern that is also a suffix for every position in the pattern.
   - This array is used to avoid redundant comparisons by allowing the algorithm to skip ahead in the pattern after a mismatch, rather than starting from scratch.
   
2. **Pattern Matching Without Backtracking**:
   - When a mismatch occurs, KMP uses the LPS array to determine the next position in the pattern to resume matching, without needing to compare characters that have already been matched.
   - This avoids the need to backtrack in the text, making the search faster.

### Example:
If you're searching for the pattern "ABABCABAB" in the text, and after matching a part of the pattern, a mismatch occurs, the LPS array helps decide how much of the pattern to skip instead of rechecking already matched characters.

### Efficiency:
- **Time Complexity**: O(n + m), where n is the length of the text, and m is the length of the pattern.
  - Precomputing the LPS array takes O(m).
  - Searching the text using the LPS array takes O(n).

This is much more efficient than the brute-force approach, which has a time complexity of O(n * m).

=============================================================

Let's walk through an example of the **Knuth-Morris-Pratt (KMP)** algorithm, including the construction of the **LPS (Longest Prefix Suffix)** array, and then I'll show you the complete algorithm.

### Example:
Let’s consider the text `ABC ABCDAB ABCDABCDABDE` and the pattern `ABCDABD`.

#### Step 1: Build the LPS Array for the Pattern `ABCDABD`
The **LPS (Longest Prefix Suffix)** array tells us the longest proper prefix of the pattern that is also a suffix for each substring.

**Pattern:** `A B C D A B D`

We will now construct the LPS array for this pattern:

1. **i = 0** (First character `A`): There is no proper prefix or suffix for the first character. So, **LPS[0] = 0**.

2. **i = 1** (Second character `B`): No proper prefix or suffix. **LPS[1] = 0**.

3. **i = 2** (Third character `C`): No proper prefix or suffix. **LPS[2] = 0**.

4. **i = 3** (Fourth character `D`): No proper prefix or suffix. **LPS[3] = 0**.

5. **i = 4** (Fifth character `A`): The character `A` is the same as the first character. The longest proper prefix that is also a suffix is "A". **LPS[4] = 1**.

6. **i = 5** (Sixth character `B`): The first two characters "AB" are a proper prefix and also a suffix. So, **LPS[5] = 2**.

7. **i = 6** (Seventh character `D`): No match after prefix "AB". So, **LPS[6] = 0**.

Thus, the **LPS array** is:

```
Pattern:  A  B  C  D  A  B  D
LPS:      0  0  0  0  1  2  0
```

### Step 2: KMP Algorithm

Now that we have the LPS array, we can use it to search the pattern in the text.

**Text:** `ABC ABCDAB ABCDABCDABDE`  
**Pattern:** `ABCDABD`

#### Algorithm:

1. Initialize two indices: `i = 0` (for text) and `j = 0` (for pattern).

2. Compare `text[i]` with `pattern[j]`:
   - If `text[i] == pattern[j]`, move both `i` and `j` forward (`i++`, `j++`).
   - If `text[i] != pattern[j]`:
     - If `j != 0`, set `j = LPS[j-1]` (this is the key step that uses the LPS array to avoid backtracking).
     - If `j == 0`, simply move `i` forward (`i++`).

3. If `j` reaches the length of the pattern (i.e., `j == pattern.length`), a match is found. Reset `j = LPS[j-1]` to look for other potential matches.

4. Continue until the entire text is scanned.

### Full Algorithm (KMP):

```javascript
function KMPSearch(pattern, text) {
  const M = pattern.length;
  const N = text.length;

  // Step 1: Build the LPS array
  const lps = buildLPSArray(pattern);

  let i = 0; // index for text
  let j = 0; // index for pattern

  while (i < N) {
    if (pattern[j] === text[i]) {
      i++;
      j++;
    }

    if (j === M) {
      console.log("Found pattern at index " + (i - j));
      j = lps[j - 1]; // Check for more matches
    }
    // mismatch after j matches
    else if (i < N && pattern[j] !== text[i]) {
      if (j !== 0) {
        j = lps[j - 1];
      } else {
        i++;
      }
    }
  }
}

// Helper function to build the LPS array
function buildLPSArray(pattern) {
  const M = pattern.length;
  const lps = new Array(M).fill(0);

  let length = 0; // length of the previous longest prefix suffix
  let i = 1;

  while (i < M) {
    if (pattern[i] === pattern[length]) {
      length++;
      lps[i] = length;
      i++;
    } else {
      if (length !== 0) {
        length = lps[length - 1];
      } else {
        lps[i] = 0;
        i++;
      }
    }
  }
  return lps;
}

// Example usage
const text = "ABC ABCDAB ABCDABCDABDE";
const pattern = "ABCDABD";
KMPSearch(pattern, text);
```

### Explanation of Example:
- When searching for `ABCDABD` in `ABC ABCDAB ABCDABCDABDE`:
  - The KMP algorithm will start by comparing characters.
  - When it reaches a mismatch, instead of backtracking, it will use the **LPS array** to skip unnecessary comparisons.
  - It finds the pattern starting at index `15` in the text.

### Summary:
- The **LPS array** helps avoid redundant checks by indicating how far back we should shift the pattern when a mismatch occurs.
- The KMP algorithm’s time complexity is **O(n + m)**, where `n` is the length of the text and `m` is the length of the pattern.