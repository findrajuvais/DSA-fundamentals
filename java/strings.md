# Strings

This section covers Strings in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a String?

In Java, a String is an immutable sequence of characters. It's a class, not a primitive type, and provides many built-in methods for manipulation.

## Declaration and Initialization

### Syntax
```java
// Using string literals (recommended)
String str = "Hello World";

// Using constructor
String str = new String("Hello World");

// Empty string
String empty = "";

// Character array to string
char[] chars = {'H', 'e', 'l', 'l', 'o'};
String str = new String(chars);
```

### Key Points
- Strings are immutable: operations create new strings.
- String literals are stored in the string pool for memory efficiency.

## Common Methods

### Length and Access
```java
String str = "Hello";
int len = str.length();  // 5
char ch = str.charAt(0);  // 'H'
```

### Substring
```java
String str = "Hello World";
String sub = str.substring(6);     // "World"
String sub2 = str.substring(0, 5); // "Hello"
```

### Comparison
```java
String s1 = "hello";
String s2 = "HELLO";
boolean equal = s1.equals(s2);           // false
boolean ignoreCase = s1.equalsIgnoreCase(s2);  // true
int compare = s1.compareTo(s2);          // positive (h > H in ASCII)
```

### Searching
```java
String str = "Hello World";
int index = str.indexOf('o');        // 4
int lastIndex = str.lastIndexOf('o'); // 7
boolean contains = str.contains("World"); // true
```

### Modification (Creates New String)
```java
String str = "Hello";
String upper = str.toUpperCase();   // "HELLO"
String lower = str.toLowerCase();   // "hello"
String replace = str.replace('l', 'x'); // "Hexxo"
String trim = "  Hello  ".trim();   // "Hello"
```

### Splitting and Joining
```java
String str = "apple,banana,cherry";
String[] parts = str.split(",");  // ["apple", "banana", "cherry"]

String joined = String.join("-", parts);  // "apple-banana-cherry"
```

### Conversion
```java
// String to char array
char[] chars = str.toCharArray();

// String to int
int num = Integer.parseInt("123");

// Int to string
String numStr = String.valueOf(123);
```

## StringBuilder for Mutable Strings

For frequent modifications, use StringBuilder (mutable, efficient).

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");     // "Hello World"
sb.insert(5, ",");       // "Hello, World"
sb.reverse();            // "dlroW ,olleH"
String result = sb.toString();
```

## Common Operations for LeetCode

### 1. Palindrome Check
```java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        if (s.charAt(left) != s.charAt(right)) return false;
        left++;
        right--;
    }
    return true;
}
```

### 2. Anagram Check
```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;
    int[] count = new int[26];
    for (char c : s.toCharArray()) count[c - 'a']++;
    for (char c : t.toCharArray()) count[c - 'a']--;
    for (int i : count) if (i != 0) return false;
    return true;
}
```

### 3. Reverse Words
```java
public String reverseWords(String s) {
    String[] words = s.trim().split("\\s+");
    StringBuilder sb = new StringBuilder();
    for (int i = words.length - 1; i >= 0; i--) {
        sb.append(words[i]);
        if (i > 0) sb.append(" ");
    }
    return sb.toString();
}
```

### 4. Longest Common Prefix
```java
public String longestCommonPrefix(String[] strs) {
    if (strs.length == 0) return "";
    String prefix = strs[0];
    for (int i = 1; i < strs.length; i++) {
        while (strs[i].indexOf(prefix) != 0) {
            prefix = prefix.substring(0, prefix.length() - 1);
            if (prefix.isEmpty()) return "";
        }
    }
    return prefix;
}
```

## Time Complexities

- Length: O(1)
- Access charAt: O(1)
- Substring: O(n)
- IndexOf: O(n)
- Comparison: O(n)
- StringBuilder operations: O(1) amortized

## LeetCode Examples

### Problem: Valid Palindrome
Check if a string is a palindrome, considering only alphanumeric characters and ignoring cases.

```java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
        if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right))) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}
```

### Problem: Group Anagrams
Group strings that are anagrams.

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

## Tips for LeetCode
- Use StringBuilder for building strings in loops.
- For character frequency, use arrays (26 for lowercase) or HashMap.
- Check for null/empty strings.
- Practice problems: 125. Valid Palindrome, 49. Group Anagrams, 3. Longest Substring Without Repeating Characters, 5. Longest Palindromic Substring.