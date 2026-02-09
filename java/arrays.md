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

---

# LeetCode Array Problems

## Easy Level

### 1. Build Array from Permutation
**Problem**: Given array `perm`, build array `ans` where `ans[i] = perm[perm[i]]`.

```java
public int[] buildArray(int[] perm) {
    int[] ans = new int[perm.length];
    for (int i = 0; i < perm.length; i++) {
        ans[i] = perm[perm[i]];
    }
    return ans;
}
```
**Time**: O(n) | **Space**: O(n)

---

### 2. Concatenation of Array
**Problem**: Concatenate array `nums` with itself.

```java
public int[] getConcatenation(int[] nums) {
    int[] ans = new int[2 * nums.length];
    for (int i = 0; i < nums.length; i++) {
        ans[i] = nums[i];
        ans[i + nums.length] = nums[i];
    }
    return ans;
}
```
**Time**: O(n) | **Space**: O(n)

---

### 3. Running Sum of 1d Array
**Problem**: Return running sum array where `returnedArray[i] = sum(nums[0]...nums[i])`.

```java
public int[] runningSum(int[] nums) {
    int[] ans = new int[nums.length];
    int sum = 0;
    for (int i = 0; i < nums.length; i++) {
        sum += nums[i];
        ans[i] = sum;
    }
    return ans;
}
```
**Time**: O(n) | **Space**: O(n)

---

### 4. Richest Customer Wealth
**Problem**: Given 2D array where each row is a customer's accounts, return richest customer's wealth.

```java
public int maximumWealth(int[][] accounts) {
    int maxWealth = 0;
    for (int[] customer : accounts) {
        int wealth = 0;
        for (int account : customer) {
            wealth += account;
        }
        maxWealth = Math.max(maxWealth, wealth);
    }
    return maxWealth;
}
```
**Time**: O(m×n) | **Space**: O(1)

---

### 5. Shuffle the Array
**Problem**: Given array `nums` of size `2n`, shuffle it as `[nums[0], nums[n], nums[1], nums[n+1], ...]`.

```java
public int[] shuffle(int[] nums, int n) {
    int[] ans = new int[2 * n];
    for (int i = 0; i < n; i++) {
        ans[2 * i] = nums[i];
        ans[2 * i + 1] = nums[n + i];
    }
    return ans;
}
```
**Time**: O(n) | **Space**: O(n)

---

### 6. Kids With the Greatest Number of Candies
**Problem**: For each kid, determine if they have the greatest number of candies after receiving extra candies.

```java
public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
    List<Boolean> result = new ArrayList<>();
    int maxCandies = 0;
    for (int candy : candies) {
        maxCandies = Math.max(maxCandies, candy);
    }
    for (int candy : candies) {
        result.add(candy + extraCandies >= maxCandies);
    }
    return result;
}
```
**Time**: O(n) | **Space**: O(n)

---

### 7. Number of Good Pairs
**Problem**: Count pairs (i, j) where i < j and nums[i] == nums[j].

```java
public int countGoodPairs(int[] nums) {
    Map<Integer, Integer> freq = new HashMap<>();
    int count = 0;
    for (int num : nums) {
        count += freq.getOrDefault(num, 0);
        freq.put(num, freq.getOrDefault(num, 0) + 1);
    }
    return count;
}
```
**Time**: O(n) | **Space**: O(n)

---

### 8. How Many Numbers Are Smaller Than the Current Number
**Problem**: For each number, count how many numbers in array are smaller.

```java
public int[] smallerNumbersThanCurrent(int[] nums) {
    int[] ans = new int[nums.length];
    for (int i = 0; i < nums.length; i++) {
        int count = 0;
        for (int j = 0; j < nums.length; j++) {
            if (nums[j] < nums[i]) count++;
        }
        ans[i] = count;
    }
    return ans;
}
```
**Time**: O(n²) | **Space**: O(n)

---

### 9. Create Target Array in the Given Order
**Problem**: Given arrays `nums` and `index`, create target array at specified indices.

```java
public int[] createTargetArray(int[] nums, int[] index) {
    List<Integer> target = new ArrayList<>();
    for (int i = 0; i < nums.length; i++) {
        target.add(index[i], nums[i]);
    }
    return target.stream().mapToInt(Integer::intValue).toArray();
}
```
**Time**: O(n²) | **Space**: O(n)

---

### 10. Check if the Sentence Is Pangram
**Problem**: Check if sentence contains every letter of the English alphabet.

```java
public boolean checkIfPangram(String sentence) {
    boolean[] letters = new boolean[26];
    for (char c : sentence.toCharArray()) {
        letters[c - 'a'] = true;
    }
    for (boolean present : letters) {
        if (!present) return false;
    }
    return true;
}
```
**Time**: O(n) | **Space**: O(1)

---

### 11. Count Items Matching a Rule
**Problem**: Count items matching all criteria from ruleKey and ruleValue.

```java
public int countMatches(List<List<String>> items, String ruleKey, String ruleValue) {
    int count = 0;
    int index = ruleKey.equals("type") ? 0 : ruleKey.equals("color") ? 1 : 2;
    for (List<String> item : items) {
        if (item.get(index).equals(ruleValue)) count++;
    }
    return count;
}
```
**Time**: O(n) | **Space**: O(1)

---

### 12. Find the Highest Altitude
**Problem**: Given gain array, find highest altitude gained (starting from 0).

```java
public int largestAltitude(int[] gain) {
    int maxAlt = 0, current = 0;
    for (int g : gain) {
        current += g;
        maxAlt = Math.max(maxAlt, current);
    }
    return maxAlt;
}
```
**Time**: O(n) | **Space**: O(1)

---

### 13. Flipping an Image
**Problem**: Invert and flip horizontal each row of a binary matrix.

```java
public int[][] flipAndInvertImage(int[][] image) {
    for (int[] row : image) {
        // Reverse
        int left = 0, right = row.length - 1;
        while (left <= right) {
            int temp = row[left];
            row[left] = row[right];
            row[right] = temp;
            left++;
            right--;
        }
        // Invert
        for (int i = 0; i < row.length; i++) {
            row[i] = row[i] == 0 ? 1 : 0;
        }
    }
    return image;
}
```
**Time**: O(m×n) | **Space**: O(1)

---

### 14. Cells with Odd Values in a Matrix
**Problem**: Count cells with odd values after incrementing rows and columns.

```java
public int oddCellsCount(int m, int n, int[][] indices) {
    int[] rowCount = new int[m];
    int[] colCount = new int[n];
    
    for (int[] op : indices) {
        rowCount[op[0]]++;
        colCount[op[1]]++;
    }
    
    int count = 0;
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if ((rowCount[i] + colCount[j]) % 2 == 1) count++;
        }
    }
    return count;
}
```
**Time**: O(m×n + k) | **Space**: O(m+n)

---

### 15. Matrix Diagonal Sum
**Problem**: Return sum of matrix diagonals (without double-counting middle).

```java
public int diagonalSum(int[][] mat) {
    int sum = 0;
    int n = mat.length;
    for (int i = 0; i < n; i++) {
        sum += mat[i][i];  // Main diagonal
        if (i != n - 1 - i) {
            sum += mat[i][n - 1 - i];  // Anti-diagonal
        }
    }
    return sum;
}
```
**Time**: O(n) | **Space**: O(1)

---

### 16. Find Numbers with Even Number of Digits
**Problem**: Count numbers that have even number of digits.

```java
public int findNumbers(int[] nums) {
    int count = 0;
    for (int num : nums) {
        if (Integer.toString(num).length() % 2 == 0) count++;
    }
    return count;
}
```
**Time**: O(n) | **Space**: O(1)

---

### 17. Transpose Matrix
**Problem**: Transpose an m×n matrix.

```java
public int[][] transpose(int[][] matrix) {
    int m = matrix.length, n = matrix[0].length;
    int[][] result = new int[n][m];
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            result[j][i] = matrix[i][j];
        }
    }
    return result;
}
```
**Time**: O(m×n) | **Space**: O(m×n)

---

### 18. Add to Array-Form of Integer
**Problem**: Add array representation and integer k.

```java
public List<Integer> addToArrayForm(int[] num, int k) {
    List<Integer> result = new ArrayList<>();
    int carry = k;
    for (int i = num.length - 1; i >= 0; i--) {
        carry += num[i];
        result.add(carry % 10);
        carry /= 10;
    }
    while (carry > 0) {
        result.add(carry % 10);
        carry /= 10;
    }
    Collections.reverse(result);
    return result;
}
```
**Time**: O(max(n, log k)) | **Space**: O(result length)

---

### 19. Maximum Population Year
**Problem**: Find year with maximum population given birth and death years.

```java
public int maximumPopulation(int[][] logs) {
    int[] years = new int[2051];
    for (int[] log : logs) {
        years[log[0]]++;
        years[log[1]]--;
    }
    int maxPop = 0, maxYear = 0, currentPop = 0;
    for (int i = 1950; i <= 2050; i++) {
        currentPop += years[i];
        if (currentPop > maxPop) {
            maxPop = currentPop;
            maxYear = i;
        }
    }
    return maxYear;
}
```
**Time**: O(n + 101) | **Space**: O(101)

---

### 20. Determine Whether Matrix Can Be Obtained By Rotation
**Problem**: Check if one matrix is rotation of another.

```java
public boolean findRotation(int[][] mat, int[][] target) {
    int n = mat.length;
    for (int rotation = 0; rotation < 4; rotation++) {
        if (Arrays.deepEquals(mat, target)) return true;
        // Rotate mat 90 degrees clockwise
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int temp = mat[i][j];
                mat[i][j] = mat[n - 1 - j][i];
                mat[n - 1 - j][i] = mat[n - 1 - i][n - 1 - j];
                mat[n - 1 - i][n - 1 - j] = mat[j][n - 1 - i];
                mat[j][n - 1 - i] = temp;
            }
        }
    }
    return false;
}
```
**Time**: O(4n²) | **Space**: O(1)

---

### 21. Two Sum (Already Covered)
See solution above.

---

### 22. Find N Unique Integers Sum up to Zero
**Problem**: Find array of n unique integers with sum 0.

```java
public int[] sumZero(int n) {
    int[] result = new int[n];
    for (int i = 0; i < n / 2; i++) {
        result[i] = -(i + 1);
        result[n - 1 - i] = i + 1;
    }
    return result;
}
```
**Time**: O(n) | **Space**: O(n)

---

### 23. Lucky Number In a Matrix
**Problem**: Find number that is minimum in row and maximum in column.

```java
public List<Integer> luckyNumbers(int[][] matrix) {
    List<Integer> result = new ArrayList<>();
    int m = matrix.length, n = matrix[0].length;
    
    int[] rowMin = new int[m];
    Arrays.fill(rowMin, Integer.MAX_VALUE);
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            rowMin[i] = Math.min(rowMin[i], matrix[i][j]);
        }
    }
    
    int[] colMax = new int[n];
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            colMax[j] = Math.max(colMax[j], matrix[i][j]);
        }
    }
    
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (matrix[i][j] == rowMin[i] && matrix[i][j] == colMax[j]) {
                result.add(matrix[i][j]);
            }
        }
    }
    return result;
}
```
**Time**: O(m×n) | **Space**: O(m+n)

---

## Medium Level

### 1. Maximum Subarray (Already Covered)
See solution above using Kadane's Algorithm.

---

### 2. Reshape the Matrix
**Problem**: Reshape m×n matrix into r×c matrix.

```java
public int[][] matrixReshape(int[][] mat, int r, int c) {
    int m = mat.length, n = mat[0].length;
    if (m * n != r * c) return mat;
    
    int[][] result = new int[r][c];
    int idx = 0;
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            result[idx / c][idx % c] = mat[i][j];
            idx++;
        }
    }
    return result;
}
```
**Time**: O(m×n) | **Space**: O(r×c)

---

### 3. Plus One
**Problem**: Add 1 to number represented as array.

```java
public int[] plusOne(int[] digits) {
    for (int i = digits.length - 1; i >= 0; i--) {
        if (digits[i] < 9) {
            digits[i]++;
            return digits;
        }
        digits[i] = 0;
    }
    int[] result = new int[digits.length + 1];
    result[0] = 1;
    return result;
}
```
**Time**: O(n) | **Space**: O(n) worst case

---

### 4. Remove Duplicates from Sorted Array
**Problem**: Remove duplicates in-place, return unique count.

```java
public int removeDuplicates(int[] nums) {
    int j = 1;
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] != nums[i - 1]) {
            nums[j++] = nums[i];
        }
    }
    return j;
}
```
**Time**: O(n) | **Space**: O(1)

---

### 5. Minimum Cost to Move Chips to The Same Position
**Problem**: Minimize cost to move chips to same position.

```java
public int minimumCost(int[] position) {
    Arrays.sort(position);
    int median = position[position.length / 2];
    int cost = 0;
    for (int pos : position) {
        cost += Math.abs(pos - median);
    }
    return cost;
}
```
**Time**: O(n log n) | **Space**: O(1)

---

### 6. Spiral Matrix
**Problem**: Return elements of m×n matrix in spiral order.

```java
public List<Integer> spiralOrder(int[][] matrix) {
    List<Integer> result = new ArrayList<>();
    if (matrix.length == 0) return result;
    
    int top = 0, bottom = matrix.length - 1;
    int left = 0, right = matrix[0].length - 1;
    
    while (top <= bottom && left <= right) {
        // Traverse right
        for (int i = left; i <= right; i++) {
            result.add(matrix[top][i]);
        }
        top++;
        
        // Traverse down
        for (int i = top; i <= bottom; i++) {
            result.add(matrix[i][right]);
        }
        right--;
        
        // Traverse left
        if (top <= bottom) {
            for (int i = right; i >= left; i--) {
                result.add(matrix[bottom][i]);
            }
            bottom--;
        }
        
        // Traverse up
        if (left <= right) {
            for (int i = bottom; i >= top; i--) {
                result.add(matrix[i][left]);
            }
            left++;
        }
    }
    return result;
}
```
**Time**: O(m×n) | **Space**: O(result)

---

### 7. Spiral Matrix II
**Problem**: Generate n×n matrix filled with elements 1 to n² in spiral order.

```java
public int[][] generateMatrix(int n) {
    int[][] matrix = new int[n][n];
    int top = 0, bottom = n - 1, left = 0, right = n - 1;
    int num = 1;
    
    while (top <= bottom && left <= right) {
        for (int i = left; i <= right; i++) {
            matrix[top][i] = num++;
        }
        top++;
        
        for (int i = top; i <= bottom; i++) {
            matrix[i][right] = num++;
        }
        right--;
        
        if (top <= bottom) {
            for (int i = right; i >= left; i--) {
                matrix[bottom][i] = num++;
            }
            bottom--;
        }
        
        if (left <= right) {
            for (int i = bottom; i >= top; i--) {
                matrix[i][left] = num++;
            }
            left++;
        }
    }
    return matrix;
}
```
**Time**: O(n²) | **Space**: O(n²)

---

### 8. Spiral Matrix III
**Problem**: Starting at given position, visit all cells in spiral order.

```java
public int[][] spiralMatrixIII(int rows, int cols, int rStart, int cStart) {
    int[][] result = new int[rows * cols][];
    int idx = 0;
    result[idx++] = new int[]{rStart, cStart};
    
    int steps = 1;
    int r = rStart, c = cStart;
    int[] directions = {0, 1, 1, 0, 0, -1, -1, 0}; // right, down, left, up
    
    for (int dir = 0; dir < 4 && idx < rows * cols; ) {
        for (int count = 0; count < steps && idx < rows * cols; count++) {
            r += directions[2 * dir];
            c += directions[2 * dir + 1];
            if (r >= 0 && r < rows && c >= 0 && c < cols) {
                result[idx++] = new int[]{r, c};
            }
        }
        dir = (dir + 1) % 4;
        if (dir % 2 == 0) steps++;
    }
    return result;
}
```
**Time**: O(rows×cols) | **Space**: O(result)

---

### 9. Set Matrix Zeroes
**Problem**: Set entire row and column to 0 if element is 0.

```java
public void setZeroes(int[][] matrix) {
    boolean firstRowZero = false, firstColZero = false;
    
    // Check first row and column
    for (int j = 0; j < matrix[0].length; j++) {
        if (matrix[0][j] == 0) firstRowZero = true;
    }
    for (int i = 0; i < matrix.length; i++) {
        if (matrix[i][0] == 0) firstColZero = true;
    }
    
    // Mark zeros using first row/col
    for (int i = 1; i < matrix.length; i++) {
        for (int j = 1; j < matrix[0].length; j++) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }
    
    // Set to zero based on marks
    for (int i = 1; i < matrix.length; i++) {
        for (int j = 1; j < matrix[0].length; j++) {
            if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                matrix[i][j] = 0;
            }
        }
    }
    
    // Handle first row and column
    if (firstRowZero) {
        for (int j = 0; j < matrix[0].length; j++) {
            matrix[0][j] = 0;
        }
    }
    if (firstColZero) {
        for (int i = 0; i < matrix.length; i++) {
            matrix[i][0] = 0;
        }
    }
}
```
**Time**: O(m×n) | **Space**: O(1)

---

### 10. Product of Array Except Self
**Problem**: Return array where each element is product of all except itself.

```java
public int[] productExceptSelf(int[] nums) {
    int[] result = new int[nums.length];
    int[] prefix = new int[nums.length];
    int[] suffix = new int[nums.length];
    
    prefix[0] = 1;
    for (int i = 1; i < nums.length; i++) {
        prefix[i] = prefix[i - 1] * nums[i - 1];
    }
    
    suffix[nums.length - 1] = 1;
    for (int i = nums.length - 2; i >= 0; i--) {
        suffix[i] = suffix[i + 1] * nums[i + 1];
    }
    
    for (int i = 0; i < nums.length; i++) {
        result[i] = prefix[i] * suffix[i];
    }
    return result;
}
```
**Time**: O(n) | **Space**: O(n)

---

### 11. Find First and Last Position of Element in Sorted Array
**Problem**: Find first and last position of target in sorted array.

```java
public int[] searchRange(int[] nums, int target) {
    int[] result = {-1, -1};
    if (nums.length == 0) return result;
    
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    if (left >= nums.length || nums[left] != target) return result;
    result[0] = left;
    
    right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] <= target) left = mid + 1;
        else right = mid - 1;
    }
    result[1] = right;
    return result;
}
```
**Time**: O(log n) | **Space**: O(1)

---

### 12. Jump Game
**Problem**: Determine if you can reach last index starting from first.

```java
public boolean canJump(int[] nums) {
    int maxReach = 0;
    for (int i = 0; i < nums.length; i++) {
        if (i > maxReach) return false;
        maxReach = Math.max(maxReach, i + nums[i]);
        if (maxReach >= nums.length - 1) return true;
    }
    return false;
}
```
**Time**: O(n) | **Space**: O(1)

---

### 13. Rotate Array
**Problem**: Rotate array k steps to right.

```java
public void rotate(int[] nums, int k) {
    k = k % nums.length;
    reverse(nums, 0, nums.length - 1);
    reverse(nums, 0, k - 1);
    reverse(nums, k, nums.length - 1);
}

private void reverse(int[] nums, int start, int end) {
    while (start < end) {
        int temp = nums[start];
        nums[start] = nums[end];
        nums[end] = temp;
        start++;
        end--;
    }
}
```
**Time**: O(n) | **Space**: O(1)

---

### 14. Sort Colors
**Problem**: Sort array with 0s, 1s, 2s in-place.

```java
public void sortColors(int[] nums) {
    int low = 0, mid = 0, high = nums.length - 1;
    while (mid <= high) {
        if (nums[mid] == 0) {
            int temp = nums[low];
            nums[low] = nums[mid];
            nums[mid] = temp;
            low++;
            mid++;
        } else if (nums[mid] == 1) {
            mid++;
        } else {
            int temp = nums[mid];
            nums[mid] = nums[high];
            nums[high] = temp;
            high--;
        }
    }
}
```
**Time**: O(n) | **Space**: O(1)

---

### 15. House Robber
**Problem**: Maximum sum of non-adjacent elements.

```java
public int rob(int[] nums) {
    if (nums.length == 0) return 0;
    if (nums.length == 1) return nums[0];
    
    int prev2 = 0, prev1 = nums[0];
    for (int i = 1; i < nums.length; i++) {
        int current = Math.max(prev1, prev2 + nums[i]);
        prev2 = prev1;
        prev1 = current;
    }
    return prev1;
}
```
**Time**: O(n) | **Space**: O(1)

---

## Hard Level

### 1. Max Value of Equation
**Problem**: Find maximum value of abs(nums[i] - nums[j]) + abs(i - j).

```java
public int maxValue(int[][] points, int k) {
    int n = points.length;
    int[] dp = new int[n];
    dp[0] = points[0][0];
    int maxVal = Integer.MIN_VALUE;
    
    for (int i = 1; i < n; i++) {
        int max = Integer.MIN_VALUE;
        for (int j = Math.max(0, i - k); j < i; j++) {
            max = Math.max(max, dp[j] - points[j][1]);
        }
        dp[i] = max + points[i][0] + points[i][1];
    }
    
    for (int i = Math.max(0, n - k); i < n; i++) {
        maxVal = Math.max(maxVal, dp[i]);
    }
    return maxVal;
}
```
**Time**: O(n×k) | **Space**: O(n)

---

### 2. First Missing Positive
**Problem**: Find smallest missing positive integer.

```java
public int firstMissingPositive(int[] nums) {
    int n = nums.length;
    
    // Mark positions
    for (int i = 0; i < n; i++) {
        while (nums[i] > 0 && nums[i] <= n && nums[nums[i] - 1] != nums[i]) {
            int idx = nums[i] - 1;
            int temp = nums[i];
            nums[i] = nums[idx];
            nums[idx] = temp;
        }
    }
    
    // Find first missing
    for (int i = 0; i < n; i++) {
        if (nums[i] != i + 1) return i + 1;
    }
    return n + 1;
}
```
**Time**: O(n) | **Space**: O(1)

---

### 3. Best Time to Buy and Sell Stock
**Problem**: Maximize profit from buying and selling stock once.

```java
public int maxProfit(int[] prices) {
    if (prices.length < 2) return 0;
    int minPrice = prices[0];
    int maxProfit = 0;
    
    for (int i = 1; i < prices.length; i++) {
        maxProfit = Math.max(maxProfit, prices[i] - minPrice);
        minPrice = Math.min(minPrice, prices[i]);
    }
    return maxProfit;
}
```
**Time**: O(n) | **Space**: O(1)

---

## Summary Table

| Difficulty | Count | Key Topics |
|---|---|---|
| Easy | 23 | Array traversal, basic manipulation, matrix operations |
| Medium | 15 | Spiral patterns, dynamic programming, two pointers |
| Hard | 3 | Graph theory, complex DP, optimization |

---

## Recommended Order for Practice
1. Start with Easy: Two Sum, Max Subarray, Remove Duplicates
2. Master Basic Matrix: Spiral Matrix, Transpose, Set Zeroes
3. Advanced Techniques: Product of Array Except Self, Jump Game
4. Hard Problems: First Missing Positive, Max Value of Equation