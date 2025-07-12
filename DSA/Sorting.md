# Sorting Algorithms Documentation

## Non-Comparison Sort

# Q What do you mean by non-comparison sort? List two non-comparison sort algorithms. 

### Definition

A **non-comparison sort** is a type of sorting algorithm that does not compare elements directly to determine their order. Instead, it uses properties of the elements (such as their digits or values as keys) to sort them. These algorithms can achieve better than O(n log n) time complexity for certain data types.

### Examples of Non-Comparison Sort Algorithms

- **Counting Sort**
    - Counts how many times each value appears.
    - Uses these counts to place each value in the correct position.
    - Works well when numbers are small and not too spread out.
    - Fast: runs in O(n + k) time.
    - Example: [4, 2, 2, 8, 3, 3, 1] → [1, 2, 2, 3, 3, 4, 8]

- **Radix Sort**
    - Sorts numbers by looking at each digit, one place at a time.
    - Usually starts from the rightmost digit.
    - Uses another stable sort (like counting sort) for each digit.
    - Good for sorting large numbers with a fixed number of digits.
    - Example: [170, 45, 75, 90, 802, 24, 2, 66] → [2, 24, 45, 66, 75, 90, 170, 802]

Other examples include **Bucket Sort**.



## Bubble Sort

### Definition

Bubble sort is a simple sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process is repeated until the list is sorted.

### Algorithm (Step-by-step)

1. Start from the first element in the list.
2. Compare the current element with the next element.
3. If the current element is greater than the next, swap them.
4. Move to the next pair and repeat steps 2-3 until the end of the list.
5. After each pass, the largest element moves ("bubbles up") to the end.
6. Repeat the process for all elements, ignoring the last sorted elements each time.
7. Stop when no swaps are needed in a pass (the list is sorted).

### Example

Suppose we have the list: 5, 2, 4, 1

- **First pass:**
  - Compare 5 and 2 → swap → 2, 5, 4, 1
  - Compare 5 and 4 → swap → 2, 4, 5, 1
  - Compare 5 and 1 → swap → 2, 4, 1, 5
- **Second pass:**
  - Compare 2 and 4 → no swap
  - Compare 4 and 1 → swap → 2, 1, 4, 5
- **Third pass:**
  - Compare 2 and 1 → swap → 1, 2, 4, 5
- Now the list is sorted: 1, 2, 4, 5

### Explanation

- Bubble sort is easy to understand and implement.
- It is not efficient for large lists because it compares and swaps many times.
- Best for small or nearly sorted lists.

### Bubble Sort in C

```c
#include <stdio.h>

void bubbleSort(int arr[], int n) {
    int i, j, temp;
    int swapped;
    for (i = 0; i < n - 1; i++) {
        swapped = 0;
        for (j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = 1;
            }
        }
        // If no two elements were swapped, the array is sorted
        if (swapped == 0)
            break;
    }
}

int main() {
    int arr[] = {5, 2, 4, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    bubbleSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

## Selection Sort

### Definition

Selection sort is a simple sorting algorithm that sorts a list by repeatedly finding the smallest (or largest) element from the unsorted part and moving it to the sorted part. It works by selecting the minimum element and swapping it with the first unsorted element.

### Algorithm (Step-by-step)

1. Start from the first element.
2. Find the smallest element in the unsorted part of the list.
3. Swap it with the first unsorted element.
4. Move the boundary of the sorted part one step forward.
5. Repeat steps 2-4 until the whole list is sorted.

### Example

#### Q12. Apply selection sort algorithm on given data to sort in ascending order: 5, 8, 6, 2, 1, 3

Suppose we have the list: 5, 8, 6, 2, 1, 3

- **First pass:**
  - Find the smallest (1). Swap with 5 → 1, 8, 6, 2, 5, 3
- **Second pass:**
  - Find the smallest in the rest (2). Swap with 8 → 1, 2, 6, 8, 5, 3
- **Third pass:**
  - Find the smallest in the rest (3). Swap with 6 → 1, 2, 3, 8, 5, 6
- **Fourth pass:**
  - Find the smallest in the rest (5). Swap with 8 → 1, 2, 3, 5, 8, 6
- **Fifth pass:**
  - Find the smallest in the rest (6). Swap with 8 → 1, 2, 3, 5, 6, 8
- Now the list is sorted: 1, 2, 3, 5, 6, 8

### Explanation

- Selection sort is easy to understand and implement.
- It always makes the same number of comparisons, even if the list is already sorted.
- Not efficient for large lists, but good for small lists.

### Selection Sort in C

```c
#include <stdio.h>

void selectionSort(int arr[], int n) {
    int i, j, min_idx, temp;
    for (i = 0; i < n - 1; i++) {
        min_idx = i;
        for (j = i + 1; j < n; j++) {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }
        // Swap the found minimum element with the first element
        temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}

int main() {
    int arr[] = {5, 8, 6, 2, 1, 3};
    int n = sizeof(arr) / sizeof(arr[0]);
    selectionSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

---

## Insertion Sort

(https://www.youtube.com/watch?v=O0VbBkUvriI&ab_channel=CS50)

### Definition

Insertion sort is a simple sorting algorithm that builds the final sorted list one item at a time. It works like sorting playing cards in your hand: you pick one card at a time and insert it into its correct position among the already sorted cards.

### Algorithm (Step-by-step)

1. Start from the second element (index 1) in the list.
2. Compare it with the elements before it.
3. Move all elements greater than the current element one position ahead.
4. Insert the current element into its correct position.
5. Repeat steps 2-4 for all elements until the list is sorted.

### Example

Suppose we have the list: 8, 5, 3, 9, 4, 1, 7

- **First pass:**
    - Take 5. Compare with 8. 5 < 8, so move 8 to the right and insert 5 at the start: 5, 8, 3, 9, 4, 1, 7
- **Second pass:**
    - Take 3. Compare with 8 and 5. 3 < 5, so move 8 and 5 to the right and insert 3 at the start: 3, 5, 8, 9, 4, 1, 7
- **Third pass:**
    - Take 9. Compare with 8,5,3. 9 > 8, so insert 9 after 8: 3, 5, 8, 9, 4, 1, 7
- **Fourth pass:**
    - Take 4. Compare with 9, 8, 5, 3. 4 < 9, 8, 5, but 4 > 3, so move 9, 8, 5 to the right and insert 4 after 3: 3, 4, 5, 8, 9, 1, 7
- **Fifth pass:**
    - Take 1. Compare with 9, 8, 5, 4, 3. 1 < all, so move all to the right and insert 1 at the start: 1, 3, 4, 5, 8, 9, 7
- **Sixth pass:**
    - Take 7. Compare with 9, 8, 5. 7 < 9, 8, but 7 > 5, so move 9 and 8 to the right and insert 7 after 5: 1, 3, 4, 5, 7, 8, 9
- Now the list is sorted: 1, 3, 4, 5, 7, 8, 9


### Explanation

- Insertion sort is easy to understand and works well for small or nearly sorted lists.
- It sorts the list in place (no extra space needed).
- It is not efficient for large lists because it may need to move many elements.

---

### Q13 & Q15. Write a program for insertion sorting. Analyze its running time?

**(Mutual Question: Q13, Q15)**

#### Simple C Program for Insertion Sort

```c
#include <stdio.h>

void insertionSort(int arr[], int n) {
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;
        // Move elements of arr[0..i-1], that are greater than key, to one position ahead
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }
}

int main() {
    int arr[] = {5, 2, 4, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    insertionSort(arr, n);
    printf("Sorted array: ");
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
    return 0;
}
```

#### Running Time Analysis

- **Best case:** O(n) (when the list is already sorted)
- **Worst case:** O(n^2) (when the list is in reverse order)
- **Average case:** O(n^2)
- **Space complexity:** O(1) (in-place)

---

### Q14. Write algorithm for Insertion sort. Also illustrate insertion sort with an example.

**Algorithm:**

1. Repeat for i = 1 to n-1:
   - Set key = arr[i]
   - Set j = i - 1
   - While j >= 0 and arr[j] > key:
     - Move arr[j] to arr[j+1]
     - Decrease j by 1
   - Place key at arr[j+1]

**Example:**
List: 7, 3, 5, 2

- Pass 1: Take 3, insert before 7 → 3, 7, 5, 2
- Pass 2: Take 5, insert between 3 and 7 → 3, 5, 7, 2
- Pass 3: Take 2, insert at start → 2, 3, 5, 7

---

## Heap Sort

### Definition

A **heap** is a special binary tree-based data structure that satisfies the heap property:

- In a **max-heap**, every parent node is greater than or equal to its children.
- In a **min-heap**, every parent node is less than or equal to its children.

**Heap sort** is a sorting algorithm that uses a heap to sort elements. It first builds a max-heap from the data, then repeatedly removes the largest element from the heap and puts it at the end of the list.

### Algorithm (Step-by-step)

1. Build a max-heap from the input data.
2. Swap the first (largest) element with the last element.
3. Reduce the heap size by one (ignore the last sorted element).
4. Heapify the root to maintain the max-heap property.
5. Repeat steps 2-4 until the heap size is 1.

### Explanation

- Heap sort is efficient and has a time complexity of O(n log n) for all cases.
- It sorts in place (no extra space needed).
- It is not a stable sort (equal elements may change order).

---

### Q16. What is a heap? How does heap sort work?

- A **heap** is a complete binary tree where each parent is greater (max-heap) or smaller (min-heap) than its children.
- **Heap sort** works by building a max-heap, then repeatedly swapping the root with the last element and reducing the heap size, maintaining the heap each time.

---

### Q17. Write heap sort algorithm and draw the max-heap only for following data 1,2,3,4,5,6,7,8,9,10

**Heap Sort Algorithm:**

1. Build a max-heap from the array.
2. For i from n-1 down to 1:
   - Swap arr[0] with arr[i]
   - Heapify arr[0..i-1]

**Max-Heap for 1,2,3,4,5,6,7,8,9,10:**

- After building max-heap: 10, 9, 7, 8, 5, 6, 3, 1, 4, 2

**Heap Tree:**

```
        10
      /    \
     9      7
    / \    / \
   8   5  6   3
  / \  /
 1  4 2
```

---

### Q18. Illustrate the execution of HEAP-SORT on the array. A = <6,14,3,25,2,10,20,7,6>

**Step 1: Build max-heap:**

- Initial array: 6, 14, 3, 25, 2, 10, 20, 7, 6
- After building max-heap: 25, 14, 20, 7, 2, 10, 3, 6, 6

**Step 2: Sort by repeatedly removing max:**

- Swap 25 and 6 → 6, 14, 20, 7, 2, 10, 3, 6, 25
- Heapify: 20, 14, 10, 7, 2, 6, 3, 6, 25
- Swap 20 and 6 → 6, 14, 10, 7, 2, 6, 3, 20, 25
- Heapify: 14, 7, 10, 6, 2, 6, 3, 20, 25
- Continue until sorted: 2, 3, 6, 6, 7, 10, 14, 20, 25

**Final sorted array:** 2, 3, 6, 6, 7, 10, 14, 20, 25

---

### Q19. Write an algorithm for heap sort technique. Illustrate with an example

**Algorithm:**

1. Build a max-heap from the array.
2. For i = n-1 down to 1:
   - Swap arr[0] with arr[i]
   - Heapify arr[0..i-1]

**Example:**
Array: 4, 1, 3, 9, 7

- Build max-heap: 9, 7, 3, 4, 1
- Swap 9 and 1: 1, 7, 3, 4, 9
- Heapify: 7, 4, 3, 1, 9
- Swap 7 and 1: 1, 4, 3, 7, 9
- Heapify: 4, 1, 3, 7, 9
- Continue until sorted: 1, 3, 4, 7, 9

---

**(Mutual Questions: Q17, Q19)**

## Quick Sort

### Definition

**Quick Sort** is a fast and efficient sorting algorithm that uses the "divide and conquer" approach. It works by selecting a "pivot" element from the list and partitioning the other elements into two groups: those less than the pivot and those greater than the pivot. The process is then repeated (recursively) for each group until the whole list is sorted.

### How Quick Sort Works (Step-by-Step):

1. Choose a pivot element from the array (often the first, last, or middle element).
2. Rearrange the array so that all elements less than the pivot come before it, and all elements greater come after it. This is called "partitioning".
3. The pivot is now in its correct sorted position.
4. Recursively apply the above steps to the sub-arrays of elements less than and greater than the pivot.
5. Continue until each sub-array has one or zero elements (which means it is sorted).

---

### Example: Quick Sort on [5, 8, 7, 6, 3, 4, 1, 9, 2, 10]

Let's sort the array step by step:

**Step 1:** Choose pivot (let's pick the last element, 10).

- Partition: All elements are less than 10, so after partition, 10 is at the end.

**Step 2:** Now, quick sort the sub-array [5, 8, 7, 6, 3, 4, 1, 9, 2] (pivot is 10).

- Choose pivot 2 (last element).
- Partition: [1] [2] [5, 8, 7, 6, 3, 4, 9]
- 2 is now in its correct position.

**Step 3:** Quick sort [1] (already sorted).

**Step 4:** Quick sort [5, 8, 7, 6, 3, 4, 9] (pivot 9).

- Partition: [5, 8, 7, 6, 3, 4] [9]
- 9 is now in its correct position.

**Step 5:** Quick sort [5, 8, 7, 6, 3, 4] (pivot 4).

- Partition: [3] [4] [5, 8, 7, 6]
- 4 is now in its correct position.

**Step 6:** Quick sort [3] (already sorted).

**Step 7:** Quick sort [5, 8, 7, 6] (pivot 6).

- Partition: [5] [6] [8, 7]
- 6 is now in its correct position.

**Step 8:** Quick sort [5] (already sorted).

**Step 9:** Quick sort [8, 7] (pivot 7).

- Partition: [7] [8]
- Both are now sorted.

**Final sorted array:** 1, 2, 3, 4, 5, 6, 7, 8, 9, 10

---

### Quick Sort Algorithm (Pseudocode)

1. If the array has 1 or 0 elements, it is already sorted.
2. Choose a pivot element.
3. Partition the array into two sub-arrays:
    - Left: elements less than pivot
    - Right: elements greater than pivot
4. Recursively apply quick sort to the left and right sub-arrays.
5. Combine the sorted sub-arrays and the pivot.

---

### Apply Quick Sort on [65, 70, 75, 80, 85, 60, 55, 40, 45]

Let's sort step by step:

1. Choose pivot (45).
2. Partition: [40] [45] [70, 75, 80, 85, 60, 55, 65]
3. Quick sort [40] (already sorted).
4. Quick sort [70, 75, 80, 85, 60, 55, 65] (pivot 65).
5. Partition: [60, 55] [65] [70, 75, 80, 85]
6. Quick sort [60, 55] (pivot 55): [55] [60]
7. Quick sort [70, 75, 80, 85] (pivot 85): [70, 75, 80] [85]
8. Quick sort [70, 75, 80] (pivot 80): [70, 75] [80]
9. Quick sort [70, 75] (pivot 75): [70] [75]

**Final sorted array:** 40, 45, 55, 60, 65, 70, 75, 80, 85

---

### Time and Space Complexity

- **Best case:** O(n log n) (when partitions are balanced)
- **Average case:** O(n log n)
- **Worst case:** O(n^2) (when partitions are very unbalanced, e.g., already sorted array)
- **Space complexity:** O(log n) due to recursion stack (in-place sorting, no extra array needed)

## Merge Sort

### Definition

**Merge Sort** is a divide-and-conquer sorting algorithm. It divides the input array into two halves, recursively sorts each half, and then merges the two sorted halves to produce the final sorted array. Merge sort is stable and guarantees O(n log n) time complexity for all cases.

### Explanation

- **Divide:** Split the array into two halves.
- **Conquer:** Recursively sort each half.
- **Combine:** Merge the two sorted halves into a single sorted array.

### Merge Sort Algorithm (Step-by-step)

1. If the array has 1 or 0 elements, it is already sorted.
2. Divide the array into two halves.
3. Recursively apply merge sort to each half.
4. Merge the two sorted halves into a single sorted array.

### Merge Sort Algorithm (Pseudocode)

```
MERGE-SORT(arr, left, right):
    if left < right:
        mid = (left + right) / 2
        MERGE-SORT(arr, left, mid)
        MERGE-SORT(arr, mid + 1, right)
        MERGE(arr, left, mid, right)
```

### Example: Sort `75, 10, 20, 70, 80, 90, 100, 40, 30, 50` using Merge Sort

**Step 1:** Divide the array  
[75, 10, 20, 70, 80] | [90, 100, 40, 30, 50]

**Step 2:** Recursively divide  
[75, 10, 20] | [70, 80] | [90, 100] | [40, 30, 50]

**Step 3:** Continue dividing  
[75, 10] | [20] | [70] | [80] | [90] | [100] | [40, 30] | [50]

**Step 4:** Sort and merge  
[10, 75] | [20] → [10, 20, 75]  
[70, 80] → [70, 80]  
[10, 20, 75] | [70, 80] → [10, 20, 70, 75, 80]

[90, 100] → [90, 100]  
[30, 40] | [50] → [30, 40, 50]  
[90, 100] | [30, 40, 50] → [30, 40, 50, 90, 100]

**Step 5:** Final merge  
[10, 20, 70, 75, 80] | [30, 40, 50, 90, 100] → [10, 20, 30, 40, 50, 70, 75, 80, 90, 100]

**Sorted array:**  
10, 20, 30, 40, 50, 70, 75, 80, 90, 100

### Time and Space Complexity

- **Time complexity:** O(n log n) in all cases
- **Space complexity:** O(n) (requires extra space for merging)