# Divide and Conquer

This section covers Divide and Conquer algorithms in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is Divide and Conquer?

Divide the problem into smaller subproblems, solve recursively, combine solutions.

## Examples

### 1. Merge Sort
```java
// As in sorting-algorithms.md
```

### 2. Quick Sort
```java
// As in sorting-algorithms.md
```

### 3. Binary Search
```java
// As in searching-algorithms.md
```

## Common Problems and Solutions

### 1. Pow(x, n)
```java
public double myPow(double x, int n) {
    if (n == 0) return 1;
    if (n < 0) {
        x = 1 / x;
        n = -n;
    }
    return powHelper(x, n);
}

private double powHelper(double x, long n) {
    if (n == 0) return 1;
    double half = powHelper(x, n / 2);
    if (n % 2 == 0) return half * half;
    return half * half * x;
}
```

### 2. Majority Element
```java
public int majorityElement(int[] nums) {
    return majorityElement(nums, 0, nums.length - 1);
}

private int majorityElement(int[] nums, int left, int right) {
    if (left == right) return nums[left];
    int mid = left + (right - left) / 2;
    int leftMajor = majorityElement(nums, left, mid);
    int rightMajor = majorityElement(nums, mid + 1, right);
    if (leftMajor == rightMajor) return leftMajor;
    int leftCount = count(nums, left, mid, leftMajor);
    int rightCount = count(nums, mid + 1, right, leftMajor);
    return leftCount > rightCount ? leftMajor : rightMajor;
}

private int count(int[] nums, int left, int right, int target) {
    int count = 0;
    for (int i = left; i <= right; i++) {
        if (nums[i] == target) count++;
    }
    return count;
}
```

### 3. Maximum Subarray
```java
public int maxSubArray(int[] nums) {
    return maxSubArray(nums, 0, nums.length - 1);
}

private int maxSubArray(int[] nums, int left, int right) {
    if (left == right) return nums[left];
    int mid = left + (right - left) / 2;
    int leftMax = maxSubArray(nums, left, mid);
    int rightMax = maxSubArray(nums, mid + 1, right);
    int crossMax = maxCrossing(nums, left, mid, right);
    return Math.max(Math.max(leftMax, rightMax), crossMax);
}

private int maxCrossing(int[] nums, int left, int mid, int right) {
    int leftSum = Integer.MIN_VALUE, sum = 0;
    for (int i = mid; i >= left; i--) {
        sum += nums[i];
        leftSum = Math.max(leftSum, sum);
    }
    int rightSum = Integer.MIN_VALUE;
    sum = 0;
    for (int i = mid + 1; i <= right; i++) {
        sum += nums[i];
        rightSum = Math.max(rightSum, sum);
    }
    return leftSum + rightSum;
}
```

## LeetCode Examples

### Problem: Pow(x, n)
```java
// As above
```

### Problem: Majority Element
```java
// As above
```

## Tips for LeetCode
- Use recursion to divide problems.
- Combine solutions carefully.
- Practice problems: 50. Pow(x, n), 169. Majority Element, 53. Maximum Subarray.