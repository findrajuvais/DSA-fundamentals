# Sorting Algorithms

This section covers Sorting Algorithms in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## Built-in Sort

### Arrays.sort()
```java
int[] arr = {3, 1, 4, 1, 5};
Arrays.sort(arr);  // {1, 1, 3, 4, 5}

// For objects
Integer[] arr = {3, 1, 4};
Arrays.sort(arr, (a, b) -> b - a);  // Descending
```

### Collections.sort()
```java
List<Integer> list = Arrays.asList(3, 1, 4);
Collections.sort(list);  // Ascending
Collections.sort(list, Collections.reverseOrder());  // Descending
```

## Bubble Sort

### Description
Repeatedly swaps adjacent elements if in wrong order.

### Code
```java
public void bubbleSort(int[] arr) {
    int n = arr.length;
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```

### Time Complexity: O(n²)

## Selection Sort

### Description
Finds minimum element and places at beginning.

### Code
```java
public void selectionSort(int[] arr) {
    int n = arr.length;
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIdx]) minIdx = j;
        }
        int temp = arr[minIdx];
        arr[minIdx] = arr[i];
        arr[i] = temp;
    }
}
```

### Time Complexity: O(n²)

## Insertion Sort

### Description
Builds sorted array one element at a time.

### Code
```java
public void insertionSort(int[] arr) {
    int n = arr.length;
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

### Time Complexity: O(n²)

## Merge Sort

### Description
Divides array into halves, sorts recursively, merges.

### Code
```java
public void mergeSort(int[] arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

private void merge(int[] arr, int left, int mid, int right) {
    int n1 = mid - left + 1, n2 = right - mid;
    int[] L = new int[n1], R = new int[n2];
    System.arraycopy(arr, left, L, 0, n1);
    System.arraycopy(arr, mid + 1, R, 0, n2);
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) arr[k++] = L[i++];
        else arr[k++] = R[j++];
    }
    while (i < n1) arr[k++] = L[i++];
    while (j < n2) arr[k++] = R[j++];
}
```

### Time Complexity: O(n log n)

## Quick Sort

### Description
Picks pivot, partitions array around it.

### Code
```java
public void quickSort(int[] arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

private int partition(int[] arr, int low, int high) {
    int pivot = arr[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
    }
    int temp = arr[i + 1];
    arr[i + 1] = arr[high];
    arr[high] = temp;
    return i + 1;
}
```

### Time Complexity: O(n log n) average, O(n²) worst

## Common Problems and Solutions

### 1. Sort Colors (Dutch National Flag)
```java
public void sortColors(int[] nums) {
    int low = 0, mid = 0, high = nums.length - 1;
    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums, low++, mid++);
        } else if (nums[mid] == 1) {
            mid++;
        } else {
            swap(nums, mid, high--);
        }
    }
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```

### 2. Kth Largest Element
```java
public int findKthLargest(int[] nums, int k) {
    Arrays.sort(nums);
    return nums[nums.length - k];
}
```

## LeetCode Examples

### Problem: Sort an Array
```java
// Use Arrays.sort or implement merge/quick sort
```

### Problem: Sort Colors
```java
// As above
```

## Tips for LeetCode
- Use built-in sort for simplicity.
- For custom sorting, use comparators.
- Counting sort for small ranges.
- Practice problems: 912. Sort an Array, 75. Sort Colors, 215. Kth Largest Element in an Array.