
![[Pasted image 20240621090208.png]]

sort 0, 1 and 2's  -
we use three pointers
0 to  (lo-1) - zeroes
lo to mid-1 - ones
mid to hi - unsorted array
hi+1 to end - twos


we apply condition on arr[mid]

![[Pasted image 20240621090230.png]]

```cpp
void sortArray(vector<int>& arr, int n) {

    int low = 0, mid = 0, high = n - 1; // 3 pointers

    while (mid <= high) {
        if (arr[mid] == 0) {
            swap(arr[low], arr[mid]);
            low++;
            mid++;
        }
        else if (arr[mid] == 1) {
            mid++;
        }
        else {
            swap(arr[mid], arr[high]);
            high--;
        }
    }
}
```




![[Pasted image 20240621090249.png]]



