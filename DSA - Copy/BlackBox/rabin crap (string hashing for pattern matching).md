it means encoding the string, 
ham chahate hai har string ke corresponding hame ek unique value mile


String hashing is widely used in competitive programming for tasks involving fast string comparisons, pattern matching, substring checking, and other operations that benefit from efficient lookups and comparisons. The idea is to convert strings into unique numerical representations (hashes) to quickly compare them.

### Key Concepts of String Hashing

1. **Hash Function**: A function that maps strings to a unique number (or as unique as possible) based on the characters in the string. A common hash function for strings is a polynomial rolling hash.

2. **Modulus**: To keep hash values manageable and avoid overflow, they are often taken modulo a large prime number (e.g., \(10^9 + 7\)). This also helps minimize hash collisions.

3. **Base (Multiplier)**: A number used to create a unique hash by weighting characters differently based on their position. Common values for the base are primes like 31, 37, or 101.

4. **Collisions**: Different strings might produce the same hash due to modulo operations. Using large primes and different bases in multiple hashes (double hashing) reduces this risk.

### Polynomial Rolling Hash

In competitive programming, a common string hash is the polynomial rolling hash. Given a string \( S = s_0, s_1, \dots, s_{n-1} \), we calculate the hash using:

\[
\text{hash}(S) = (s_0 \times p^0 + s_1 \times p^1 + \dots + s_{n-1} \times p^{n-1}) \mod m
\]

where:
- \( p \) is the base (e.g., 31).
- \( m \) is a large prime (e.g., \(10^9 + 7\)).

### Why Competitive Programmers Use String Hashing

- **Efficient Comparisons**: Hashing reduces complex string comparison to simple integer comparison.
- **Substring Matching**: Hashing allows checking if two substrings are the same in \( O(1) \) by comparing their hashes.
- **Pattern Matching**: Algorithms like Rabin-Karp use hashing to search for patterns in a string efficiently.

### Implementation of String Hashing in C++

Here’s how you can implement a rolling hash in C++ for common operations like substring comparison.

```cpp
#include <iostream>
#include <vector>

using namespace std;

const int P = 31;                // Base (a small prime)
const int MOD = 1e9 + 7;         // Modulus (a large prime)
vector<long long> power;          // To store powers of P

void precompute_powers(int n) {
    power.resize(n);
    power[0] = 1;
    for (int i = 1; i < n; i++)
        power[i] = (power[i - 1] * P) % MOD;
}

vector<long long> compute_hashes(const string &s) {
    int n = s.size();
    vector<long long> hashes(n + 1, 0); // hashes[i] is hash of prefix ending at i-1
    for (int i = 0; i < n; i++)
        hashes[i + 1] = (hashes[i] + (s[i] - 'a' + 1) * power[i]) % MOD;
    return hashes;
}

long long substring_hash(int left, int right, const vector<long long> &hashes) {
    long long hash_value = (hashes[right + 1] - hashes[left] + MOD) % MOD;
    hash_value = (hash_value * power[power.size() - left - 1]) % MOD;
    return hash_value;
}

int main() {
    string s = "hello";
    precompute_powers(s.size());

    // Compute prefix hashes for the string
    vector<long long> hashes = compute_hashes(s);

    // Example: Compare if s[0:2] == s[3:4] (Checking "hel" == "lo")
    int left1 = 0, right1 = 2;
    int left2 = 3, right2 = 4;
    if (substring_hash(left1, right1, hashes) == substring_hash(left2, right2, hashes))
        cout << "Substrings are equal\n";
    else
        cout << "Substrings are not equal\n";

    return 0;
}
```

### Explanation of Code

1. **Power Array**: `power` stores powers of \( p \) modulo \( m \). It’s precomputed to save time when calculating substring hashes.
2. **Compute Hashes**: `compute_hashes` generates prefix hashes. `hashes[i]` represents the hash of the substring \( s[0:i-1] \).
3. **Substring Hash**: `substring_hash` calculates the hash of a substring `s[left:right]` by subtracting prefix hashes and adjusting for the position in the string.

### Applications in Competitive Programming

1. **Substring Checking**: Quickly check if two substrings are identical by comparing their hashes.
2. **Pattern Matching**: Use hashing in algorithms like Rabin-Karp to match patterns in \( O(N) \) time.
3. **Efficient Storage**: Store hashes instead of strings for memory-efficient solutions in large datasets.

### Tips for Using String Hashing in C++

1. **Use a Large Prime for MOD**: This reduces collisions and makes hashes more unique.
2. **Double Hashing**: For critical applications, use two different primes (like 31 and 53) for double hashing to further minimize collision chances.
3. **Prefix Hashing**: Precompute prefix hashes for \( O(1) \) substring hash calculation.

String hashing is an essential technique for competitive programming due to its efficiency, making it ideal for tasks requiring fast string manipulations and comparisons.