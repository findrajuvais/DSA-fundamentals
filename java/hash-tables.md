# Hash Tables

This section covers Hash Tables in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a Hash Table?

A hash table (or hash map) is a data structure that stores key-value pairs with average O(1) time complexity for insertions, deletions, and lookups. It uses a hash function to map keys to indices.

## Implementation in Java

### Using HashMap
```java
import java.util.HashMap;
import java.util.Map;

Map<String, Integer> map = new HashMap<>();
map.put("apple", 1);     // Insert
int value = map.get("apple");  // 1, get value
boolean contains = map.containsKey("apple"); // true
map.remove("apple");     // Remove
boolean empty = map.isEmpty(); // false
int size = map.size();   // 0
```

### Using HashSet (for keys only)
```java
import java.util.HashSet;
import java.util.Set;

Set<String> set = new HashSet<>();
set.add("apple");        // Add
boolean contains = set.contains("apple"); // true
set.remove("apple");     // Remove
```

## Basic Operations

- **put(key, value)**: Insert or update. O(1) average
- **get(key)**: Retrieve value. O(1) average
- **remove(key)**: Delete entry. O(1) average
- **containsKey(key)**: Check if key exists. O(1) average
- **keySet()**: Get all keys.
- **values()**: Get all values.
- **entrySet()**: Get all key-value pairs.

## Common Problems and Solutions

### 1. Two Sum
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

### 2. Group Anagrams
```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> map = new HashMap<>();
    for (String str : strs) {
        char[] chars = str.toCharArray();
        Arrays.sort(chars);
        String key = new String(chars);
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(str);
    }
    return new ArrayList<>(map.values());
}
```

### 3. Longest Substring Without Repeating Characters
```java
public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> map = new HashMap<>();
    int maxLength = 0;
    int left = 0;
    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        if (map.containsKey(c)) {
            left = Math.max(left, map.get(c) + 1);
        }
        map.put(c, right);
        maxLength = Math.max(maxLength, right - left + 1);
    }
    return maxLength;
}
```

### 4. Top K Frequent Elements
```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> count = new HashMap<>();
    for (int num : nums) {
        count.put(num, count.getOrDefault(num, 0) + 1);
    }
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> b[1] - a[1]);
    for (Map.Entry<Integer, Integer> entry : count.entrySet()) {
        pq.add(new int[]{entry.getKey(), entry.getValue()});
    }
    int[] result = new int[k];
    for (int i = 0; i < k; i++) {
        result[i] = pq.poll()[0];
    }
    return result;
}
```

### 5. Valid Sudoku
```java
public boolean isValidSudoku(char[][] board) {
    Set<String> seen = new HashSet<>();
    for (int i = 0; i < 9; i++) {
        for (int j = 0; j < 9; j++) {
            char num = board[i][j];
            if (num != '.') {
                if (!seen.add(num + " in row " + i) ||
                    !seen.add(num + " in col " + j) ||
                    !seen.add(num + " in box " + i/3 + "-" + j/3)) {
                    return false;
                }
            }
        }
    }
    return true;
}
```

## Time Complexities

- Insert/Get/Remove: O(1) average, O(n) worst case
- Contains: O(1) average

## LeetCode Examples

### Problem: Two Sum
```java
// As above
```

### Problem: Contains Duplicate II
```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        if (map.containsKey(nums[i]) && i - map.get(nums[i]) <= k) {
            return true;
        }
        map.put(nums[i], i);
    }
    return false;
}
```

## Tips for LeetCode
- Use HashMap for key-value, HashSet for unique elements.
- For frequency counts, use map.
- Sliding window with map for substring problems.
- Practice problems: 1. Two Sum, 49. Group Anagrams, 3. Longest Substring Without Repeating Characters, 347. Top K Frequent Elements, 36. Valid Sudoku.