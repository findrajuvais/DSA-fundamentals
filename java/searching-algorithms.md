# Searching Algorithms

This section covers Searching Algorithms in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## Linear Search

### Description
Checks each element sequentially until found.

### Code
```java
public int linearSearch(int[] arr, int target) {
    for (int i = 0; i < arr.length; i++) {
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}
```

### Time Complexity: O(n)

## Binary Search

### Description
Works on sorted arrays. Divides search space in half each time.

### Iterative
```java
public int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

### Recursive
```java
public int binarySearchRecursive(int[] arr, int target, int left, int right) {
    if (left > right) return -1;
    int mid = left + (right - left) / 2;
    if (arr[mid] == target) return mid;
    if (arr[mid] < target) return binarySearchRecursive(arr, target, mid + 1, right);
    return binarySearchRecursive(arr, target, left, mid - 1);
}
```

### Time Complexity: O(log n)

## Common Problems and Solutions

### 1. Search in Rotated Sorted Array
```java
public int search(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        if (nums[left] <= nums[mid]) {
            if (target >= nums[left] && target < nums[mid]) right = mid - 1;
            else left = mid + 1;
        } else {
            if (target > nums[mid] && target <= nums[right]) left = mid + 1;
            else right = mid - 1;
        }
    }
    return -1;
}
```

### 2. Find First and Last Position of Element in Sorted Array
```java
public int[] searchRange(int[] nums, int target) {
    int[] result = {-1, -1};
    result[0] = findFirst(nums, target);
    result[1] = findLast(nums, target);
    return result;
}

private int findFirst(int[] nums, int target) {
    int left = 0, right = nums.length - 1, first = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] >= target) {
            if (nums[mid] == target) first = mid;
            right = mid - 1;
        } else left = mid + 1;
    }
    return first;
}

private int findLast(int[] nums, int target) {
    int left = 0, right = nums.length - 1, last = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] <= target) {
            if (nums[mid] == target) last = mid;
            left = mid + 1;
        } else right = mid - 1;
    }
    return last;
}
```

### 3. Search Insert Position
```java
public int searchInsert(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return left;
}
```

## LeetCode Examples

### Problem: Binary Search
```java
// As above
```

### Problem: Search in Rotated Sorted Array
```java
// As above
```

## Tips for LeetCode
- Use binary search on sorted arrays.
- For rotated arrays, check which half is sorted.
- For finding bounds, use two binary searches.
- Practice problems: 704. Binary Search, 33. Search in Rotated Sorted Array, 34. Find First and Last Position of Element in Sorted Array, 35. Search Insert Position.