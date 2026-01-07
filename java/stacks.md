# Stacks

This section covers Stacks in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a Stack?

A stack is a linear data structure that follows the Last In, First Out (LIFO) principle. Elements are added and removed from the top.

## Implementation in Java

### Using Stack Class
```java
import java.util.Stack;

Stack<Integer> stack = new Stack<>();
stack.push(1);     // Add to top
stack.push(2);
int top = stack.peek();  // 2, without removing
int popped = stack.pop(); // 2, removes and returns
boolean empty = stack.isEmpty(); // false
int size = stack.size(); // 1
```

### Using Deque (Recommended for better performance)
```java
import java.util.Deque;
import java.util.ArrayDeque;

Deque<Integer> stack = new ArrayDeque<>();
stack.push(1);
stack.push(2);
int top = stack.peek();  // 2
int popped = stack.pop(); // 2
```

## Basic Operations

- **push(element)**: Add element to top. O(1)
- **pop()**: Remove and return top element. O(1)
- **peek()**: Return top element without removing. O(1)
- **isEmpty()**: Check if stack is empty. O(1)
- **size()**: Return number of elements. O(1)

## Common Problems and Solutions

### 1. Valid Parentheses
```java
public boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    for (char c : s.toCharArray()) {
        if (c == '(' || c == '{' || c == '[') {
            stack.push(c);
        } else {
            if (stack.isEmpty()) return false;
            char top = stack.pop();
            if ((c == ')' && top != '(') ||
                (c == '}' && top != '{') ||
                (c == ']' && top != '[')) {
                return false;
            }
        }
    }
    return stack.isEmpty();
}
```

### 2. Reverse String
```java
public String reverseString(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    for (char c : s.toCharArray()) {
        stack.push(c);
    }
    StringBuilder sb = new StringBuilder();
    while (!stack.isEmpty()) {
        sb.append(stack.pop());
    }
    return sb.toString();
}
```

### 3. Evaluate Reverse Polish Notation
```java
public int evalRPN(String[] tokens) {
    Deque<Integer> stack = new ArrayDeque<>();
    for (String token : tokens) {
        if (token.equals("+")) {
            stack.push(stack.pop() + stack.pop());
        } else if (token.equals("-")) {
            int b = stack.pop(), a = stack.pop();
            stack.push(a - b);
        } else if (token.equals("*")) {
            stack.push(stack.pop() * stack.pop());
        } else if (token.equals("/")) {
            int b = stack.pop(), a = stack.pop();
            stack.push(a / b);
        } else {
            stack.push(Integer.parseInt(token));
        }
    }
    return stack.pop();
}
```

### 4. Next Greater Element
```java
public int[] nextGreaterElement(int[] nums1, int[] nums2) {
    Map<Integer, Integer> map = new HashMap<>();
    Deque<Integer> stack = new ArrayDeque<>();
    for (int num : nums2) {
        while (!stack.isEmpty() && stack.peek() < num) {
            map.put(stack.pop(), num);
        }
        stack.push(num);
    }
    int[] result = new int[nums1.length];
    for (int i = 0; i < nums1.length; i++) {
        result[i] = map.getOrDefault(nums1[i], -1);
    }
    return result;
}
```

### 5. Min Stack (Design)
```java
class MinStack {
    private Deque<Integer> stack;
    private Deque<Integer> minStack;

    public MinStack() {
        stack = new ArrayDeque<>();
        minStack = new ArrayDeque<>();
    }

    public void push(int val) {
        stack.push(val);
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }

    public void pop() {
        if (stack.pop().equals(minStack.peek())) {
            minStack.pop();
        }
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return minStack.peek();
    }
}
```

## Time Complexities

- All operations: O(1)

## LeetCode Examples

### Problem: Valid Parentheses
```java
// As above
```

### Problem: Min Stack
```java
// As above
```

### Problem: Daily Temperatures
```java
public int[] dailyTemperatures(int[] temperatures) {
    int[] result = new int[temperatures.length];
    Deque<Integer> stack = new ArrayDeque<>();
    for (int i = 0; i < temperatures.length; i++) {
        while (!stack.isEmpty() && temperatures[stack.peek()] < temperatures[i]) {
            int idx = stack.pop();
            result[idx] = i - idx;
        }
        stack.push(i);
    }
    return result;
}
```

## Tips for LeetCode
- Use Deque instead of Stack for better performance.
- Monotonic stack for next greater/smaller problems.
- For min/max stack, use auxiliary stack.
- Practice problems: 20. Valid Parentheses, 155. Min Stack, 739. Daily Temperatures, 150. Evaluate Reverse Polish Notation, 496. Next Greater Element I.