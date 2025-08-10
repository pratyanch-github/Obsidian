
---

## **What is a Heap?**

- A **heap** is a specialized tree-based data structure that satisfies the **heap property**:
    - **Max-Heap**: Parent nodes are always greater than or equal to their children.
    - **Min-Heap**: Parent nodes are always smaller than or equal to their children.
- It is a **complete binary tree**, meaning all levels are fully filled except possibly the last, which is filled from left to right.

---

### **Applications of Heaps**

1. **Priority Queues**: Efficiently retrieve the highest/lowest priority element.
2. **Heap Sort**: A sorting algorithm based on heap.
3. **Kth Largest/Smallest Element**: Frequently used in interview problems.
4. **Merging K Sorted Arrays/Lists**.
5. **Median of a Stream**: Using a combination of Min-Heap and Max-Heap.

---

## **Heap Operations and Time Complexities**

|Operation|Description|Time Complexity|Explanation|
|---|---|---|---|
|**Insert** (Push)|Add a new element to the heap.|**O(log n)**|Requires "heapify up" to maintain heap property.|
|**Extract Max/Min**|Remove and return the root element (max/min).|**O(log n)**|Requires "heapify down" to maintain heap property.|
|**Peek**|Return the root element (max/min) without removing it.|**O(1)**|Simply returns the root.|
|**Build Heap**|Build a heap from an unsorted array.|**O(n)**|Done via heapify process in reverse level order.|
|**Heap Sort**|Use heap to sort an array.|**O(n log n)**|Repeatedly extract max/min.|

---

### **Heap Implementation**

Heaps are typically implemented using an array:

- For a node at index `i`  in `0` based indexing:
    - **Left Child**: `2i + 1`
    - **Right Child**: `2i + 2`
    - **Parent**: `(i - 1) // 2`

---

Let's break it down step-by-step and go into detail about **heapify**, **heapify up/down**, and the key heap operations such as building a heap, inserting, deleting, and peeking.

---

### **What is Heapify?**

Heapify is the process of reorganizing the elements in a heap to maintain the **heap property** (either Max-Heap or Min-Heap). It's crucial for building a heap, inserting elements, and deleting elements.

#### **Types of Heapify**

1. **Heapify Up (Percolate Up)**:
    
    - Used when you insert a new element into the heap.
    - The newly added element is compared with its parent, and if it violates the heap property, it's swapped with the parent.
    - This continues until the heap property is restored or the root is reached.
2. **Heapify Down (Percolate Down)**:
    
    - Used when you remove the root element (max/min).
    - The last element is moved to the root, and it is compared with its children.
    - If the heap property is violated, it is swapped with the larger/smaller child (for Max/Min Heap).
    - This continues until the heap property is restored or a leaf node is reached.

---

### **Building a Heap from an Unsorted Array**

The algorithm to build a heap from an unsorted array is called the **Heapify Process** or **Heap Construction Algorithm**. It transforms an unsorted array into a valid heap.

#### **How It Works**

1. **Start from the last non-leaf node** (located at `n // 2 - 1`, where `n` is the size of the array).
2. Perform **heapify down** for each node from right to left and bottom to top.
3. This ensures the heap property is satisfied for all nodes.

#### **Time Complexity**

- While each heapify down operation can take **O(log n)**, building the heap for all nodes together is **O(n)** because the depth of heapify decreases for lower levels. The actual work done is proportional to the sum of node depths, which simplifies to **O(n)**.

---
### Summary of Operations with Theory

1. **Building a Heap**:
    - Use the heapify process in reverse level order. **Time Complexity: O(n)**.
2. **Insert**:
    - Add element at the end and heapify up. **Time Complexity: O(log n)**.
3. **Delete (Extract Max/Min)**:
    - Replace root with last element, remove last, and heapify down. **Time Complexity: O(log n)**.
4. **Peek**:
    - Return the root. **Time Complexity: O(1)**.

---

Here's a detailed breakdown of heap operations implemented in **C++**. The code uses the STL vector to represent the heap, as it provides dynamic resizing and easy indexing.

---

### **Building a max Heap (Heap Construction Algorithm)**

We use a **heapify down** process starting from the last non-leaf node to build the heap. This ensures that all nodes satisfy the heap property.

#### **Code for Building a  Max Heap**

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Function to perform heapify down
void heapifyDown(vector<int>& heap, int n, int i) {
    int largest = i;              // Assume the root is the largest
    int left = 2 * i + 1;         // Left child index
    int right = 2 * i + 2;        // Right child index

    // Compare with left child
    if (left < n && heap[left] > heap[largest]) {
        largest = left;
    }

    // Compare with right child
    if (right < n && heap[right] > heap[largest]) {
        largest = right;
    }

    // If the largest is not the root
    if (largest != i) {
        swap(heap[i], heap[largest]); // Swap with the largest child
        heapifyDown(heap, n, largest); // Recursively heapify the affected subtree
    }
}

// Function to build a heap from an unsorted array
void buildHeap(vector<int>& heap) {
    int n = heap.size();
    // Start from the last non-leaf node and heapify down each node
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapifyDown(heap, n, i);
    }
}

// Function to print the heap
void printHeap(const vector<int>& heap) {
    for (int val : heap) {
        cout << val << " ";
    }
    cout << endl;
}

int main() {
    vector<int> heap = {4, 10, 3, 5, 1};
    buildHeap(heap);
    cout << "Max-Heap: ";
    printHeap(heap);
    return 0;
}
```

---

### **Insert Operation**

1. Add the new element at the end of the array (heap).
2. Perform **heapify up** to restore the heap property.

#### **Code for Insert**

```cpp
// Function to perform heapify up
void heapifyUp(vector<int>& heap, int i) {
    while (i > 0) {
        int parent = (i - 1) / 2;
        if (heap[i] > heap[parent]) { // Max-Heap condition
            swap(heap[i], heap[parent]);
            i = parent;
        } else {
            break;
        }
    }
}

// Function to insert a new value into the heap
void insert(vector<int>& heap, int value) {
    heap.push_back(value); // Add the value at the end
    heapifyUp(heap, heap.size() - 1); // Restore heap property
}

int main() {
    vector<int> heap = {10, 5, 3, 4, 1};
    buildHeap(heap);
    cout << "Max-Heap before insertion: ";
    printHeap(heap);
    
    insert(heap, 15);
    cout << "Max-Heap after insertion: ";
    printHeap(heap);
    return 0;
}
```

---

### **Delete Operation (Extract Max)**

1. Replace the root (max element) with the last element in the heap.
2. Remove the last element.
3. Perform **heapify down** from the root to restore the heap property.

#### **Code for Delete**

```cpp
// Function to extract the maximum element (root)
int extractMax(vector<int>& heap) {
    if (heap.empty()) {
        throw runtime_error("Heap is empty!");
    }
    int root = heap[0];            // Store the root
    heap[0] = heap.back();         // Replace root with the last element
    heap.pop_back();               // Remove the last element
    heapifyDown(heap, heap.size(), 0); // Restore heap property
    return root;
}

int main() {
    vector<int> heap = {15, 10, 3, 4, 1};
    buildHeap(heap);
    cout << "Max-Heap before extraction: ";
    printHeap(heap);
    
    int maxElement = extractMax(heap);
    cout << "Extracted max: " << maxElement << endl;
    cout << "Max-Heap after extraction: ";
    printHeap(heap);
    return 0;
}
```

---

### **Peek Operation**

Simply return the root element, which is the first element in the array (heap).

#### **Code for Peek**

```cpp
// Function to return the maximum element (root)
int peek(const vector<int>& heap) {
    if (heap.empty()) {
        throw runtime_error("Heap is empty!");
    }
    return heap[0];
}

int main() {
    vector<int> heap = {15, 10, 3, 4, 1};
    buildHeap(heap);
    cout << "Max-Heap: ";
    printHeap(heap);
    
    cout << "Top element (peek): " << peek(heap) << endl;
    return 0;
}
```

---

### **Heap Sort**

Use the heap to sort an array by repeatedly extracting the maximum element and rebuilding the heap.

#### **Code for Heap Sort**

```cpp
// Function to perform heap sort
void heapSort(vector<int>& arr) {
    buildHeap(arr); // Step 1: Build a max-heap
    int n = arr.size();
    for (int i = n - 1; i > 0; i--) {
        swap(arr[0], arr[i]);  // Move the root to the end
        heapifyDown(arr, i, 0); // Reduce the heap size and heapify the root
    }
}

int main() {
    vector<int> arr = {4, 10, 3, 5, 1};
    cout << "Original array: ";
    printHeap(arr);
    
    heapSort(arr);
    cout << "Sorted array: ";
    printHeap(arr);
    return 0;
}
```

---

### **Summary of Time Complexities**

|Operation|Description|Time Complexity|
|---|---|---|
|**Insert**|Add a new element and heapify up|**O(log n)**|
|**Extract Max**|Remove root and heapify down|**O(log n)**|
|**Peek**|Return the root element|**O(1)**|
|**Build Heap**|Build a heap from an unsorted array|**O(n)**|
|**Heap Sort**|Sort the array using heap operations|**O(n log n)**|

Let me know if you'd like to explore more, such as implementing a Min-Heap or solving specific heap-based problems!