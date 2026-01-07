# Arrays

This section covers Arrays in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is an Array?

An array is a fixed-size, contiguous block of memory that stores elements of the same type. In Java, arrays are objects and provide random access to elements via indices.

## Declaration and Initialization

### Syntax
```java
// Declare an array
int[] arr;

// Initialize with size
arr = new int[5];  // Creates array of size 5, default values 0

// Declare and initialize together
int[] arr = new int[5];

// Initialize with values
int[] arr = {1, 2, 3, 4, 5};

// 2D Arrays
int[][] matrix = new int[3][4];
int[][] matrix = {{1,2},{3,4},{5,6}};
```

### Key Points
- Arrays have fixed size once created.
- Indices start from 0.
- Default values: 0 for int, false for boolean, null for objects.

## Accessing Elements

```java
int[] arr = {10, 20, 30, 40, 50};

// Access element at index 2
int value = arr[2];  // 30

// Modify element
arr[0] = 100;  // Now {100, 20, 30, 40, 50}
```

## Common Methods and Properties

- `arr.length`: Returns the size of the array (not a method, it's a property).
- No built-in methods like add/remove; use loops or copy arrays.

### Useful Methods from Arrays Class
```java
import java.util.Arrays;

// Sort an array
int[] arr = {3, 1, 4, 1, 5};
Arrays.sort(arr);  // {1, 1, 3, 4, 5}

// Binary search (array must be sorted)
int index = Arrays.binarySearch(arr, 4);  // Returns index of 4

// Fill array with value
Arrays.fill(arr, 0);  // All elements become 0

// Copy array
int[] copy = Arrays.copyOf(arr, arr.length);

// Convert to string
String str = Arrays.toString(arr);  // "[1, 1, 3, 4, 5]"
```

## Common Operations for LeetCode

### 1. Traversal
```java
int[] arr = {1, 2, 3, 4, 5};

// Forward traversal
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}

// Enhanced for loop
for (int num : arr) {
    System.out.println(num);
}
```

### 2. Finding Maximum/Minimum
```java
int[] arr = {3, 1, 4, 1, 5};
int max = Integer.MIN_VALUE;
int min = Integer.MAX_VALUE;

for (int num : arr) {
    max = Math.max(max, num);
    min = Math.min(min, num);
}
```

### 3. Linear Search
```java
public int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;  // Not found
}
```

### 4. Two Pointer Technique
```java
// Reverse array
public void reverse(int[] arr) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}

// Check if array is sorted
public boolean isSorted(int[] arr) {
    for (int i = 1; i < arr.length; i++) {
        if (arr[i] < arr[i-1]) return false;
    }
    return true;
}
```

### 5. Prefix Sum
```java
// Compute prefix sum
public int[] prefixSum(int[] arr) {
    int[] prefix = new int[arr.length + 1];
    for (int i = 1; i <= arr.length; i++) {
        prefix[i] = prefix[i-1] + arr[i-1];
    }
    return prefix;
}

// Range sum query: sum from index l to r (inclusive)
public int rangeSum(int[] prefix, int l, int r) {
    return prefix[r+1] - prefix[l];
}
```

## Time Complexities

- Access: O(1)
- Search (unsorted): O(n)
- Search (sorted): O(log n) with binary search
- Insertion/Deletion: O(n) (need to shift elements)
- Sorting: O(n log n)

## LeetCode Examples

### Problem: Two Sum
Given an array of integers `nums` and an integer `target`, return indices of two numbers that add up to `target`.

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{-1, -1};
}
```

### Problem: Maximum Subarray (Kadane's Algorithm)
Find the contiguous subarray with the largest sum.

```java
public int maxSubArray(int[] nums) {
    int maxSoFar = nums[0];
    int maxEndingHere = nums[0];
    for (int i = 1; i < nums.length; i++) {
        maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
        maxSoFar = Math.max(maxSoFar, maxEndingHere);
    }
    return maxSoFar;
}
```

## Tips for LeetCode
- Always check for edge cases: empty array, single element, duplicates.
- Use two pointers for sorted arrays or to optimize space.
- For frequency counts, use arrays if range is small, else HashMap.
- Practice problems: 1. Two Sum, 53. Maximum Subarray, 217. Contains Duplicate, 238. Product of Array Except Self.