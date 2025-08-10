
Hame ek tree diya hua hai , us tree ko flat karke ek array bana lenge, taki ham sare subtrees par us array ki madat se query and updates perform kar sake.

Us banaye hue array me sare subtrees ek contiguous range ko correspond karte hai.

If we can preprocess a rooted tree such that every subtree corresponds to a contiguous range on an array, we can do updates and range queries on it!

Here's the code we're going to use to perform a Euler Tour on the graph. Notice that it follows the same general structure as a normal depth-first search. It's just that in this algorithm, we're keeping a few auxiliary variables we're going to use later on.


![[{B96D8043-1B28-4437-9A51-7A8F24E70309}.png]]

euler tour karne ke baad har node ke liye hame ek start and end time mil jata hai , ye start and end point  represent karte hai array indices [start, end] and ye subarray hi node ke corresponding wala subtree hai, 

https://usaco.guide/gold/tree-euler?lang=cpp  -- detailed dry run . 

```
#include <iostream>
#include <vector>

using std::vector;

// The graph represented as an adjacency list (0-indexed)
vector<vector<int>> neighbors{{1, 2}, {0}, {0, 3, 4}, {2}, {2}};
vector<int> start(neighbors.size());
vector<int> end(neighbors.size());
int timer = 0;

void euler_tour(int at, int prev) {
	start[at] = timer++;
	for (int n : neighbors[at]) {
		if (n != prev) { euler_tour(n, at); }
	}
	end[at] = timer;
}
```


<video controls>
  <source src="https://usaco.guide/animations/euler_tour.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>


