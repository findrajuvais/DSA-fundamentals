# Deque

This section covers Deque (Double-Ended Queue) in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a Deque?

A deque (double-ended queue) allows insertion and deletion from both ends. It can be used as both stack and queue.

## Implementation in Java

### Using Deque Interface with ArrayDeque
```java
import java.util.Deque;
import java.util.ArrayDeque;

Deque<Integer> deque = new ArrayDeque<>();
deque.addFirst(1);   // Add to front
deque.addLast(2);    // Add to rear
int front = deque.peekFirst();  // 1
int rear = deque.peekLast();    // 2
int removeFront = deque.pollFirst(); // 1
int removeRear = deque.pollLast();   // 2
boolean empty = deque.isEmpty();
int size = deque.size();
```

## Basic Operations

- **addFirst(element)** / **offerFirst(element)**: Add to front. O(1)
- **addLast(element)** / **offerLast(element)**: Add to rear. O(1)
- **pollFirst()** / **removeFirst()**: Remove and return front. O(1)
- **pollLast()** / **removeLast()**: Remove and return rear. O(1)
- **peekFirst()**: Return front without removing. O(1)
- **peekLast()**: Return rear without removing. O(1)
- **isEmpty()**: Check if empty. O(1)
- **size()**: Return size. O(1)

## Common Problems and Solutions

### 1. Sliding Window Maximum
```java
public int[] maxSlidingWindow(int[] nums, int k) {
    if (nums == null || nums.length == 0) return new int[0];
    int[] result = new int[nums.length - k + 1];
    Deque<Integer> deque = new ArrayDeque<>();
    for (int i = 0; i < nums.length; i++) {
        // Remove elements out of window
        while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
            deque.pollFirst();
        }
        // Remove smaller elements
        while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
            deque.pollLast();
        }
        deque.addLast(i);
        if (i >= k - 1) {
            result[i - k + 1] = nums[deque.peekFirst()];
        }
    }
    return result;
}
```

### 2. Design Circular Deque
```java
class MyCircularDeque {
    private int[] deque;
    private int front, rear, size, capacity;

    public MyCircularDeque(int k) {
        capacity = k;
        deque = new int[k];
        front = 0;
        rear = 0;
        size = 0;
    }

    public boolean insertFront(int value) {
        if (isFull()) return false;
        front = (front - 1 + capacity) % capacity;
        deque[front] = value;
        size++;
        return true;
    }

    public boolean insertLast(int value) {
        if (isFull()) return false;
        deque[rear] = value;
        rear = (rear + 1) % capacity;
        size++;
        return true;
    }

    public boolean deleteFront() {
        if (isEmpty()) return false;
        front = (front + 1) % capacity;
        size--;
        return true;
    }

    public boolean deleteLast() {
        if (isEmpty()) return false;
        rear = (rear - 1 + capacity) % capacity;
        size--;
        return true;
    }

    public int getFront() {
        if (isEmpty()) return -1;
        return deque[front];
    }

    public int getRear() {
        if (isEmpty()) return -1;
        return deque[(rear - 1 + capacity) % capacity];
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }
}
```

### 3. Palindrome Check with Deque
```java
public boolean isPalindrome(String s) {
    Deque<Character> deque = new ArrayDeque<>();
    for (char c : s.toCharArray()) {
        if (Character.isLetterOrDigit(c)) {
            deque.addLast(Character.toLowerCase(c));
        }
    }
    while (deque.size() > 1) {
        if (deque.pollFirst() != deque.pollLast()) {
            return false;
        }
    }
    return true;
}
```

## Time Complexities

- All operations: O(1)

## LeetCode Examples

### Problem: Sliding Window Maximum
```java
// As above
```

### Problem: Design Circular Deque
```java
// As above
```

## Tips for LeetCode
- Use ArrayDeque for efficient operations.
- Monotonic deque for sliding window problems.
- For circular, use modular arithmetic.
- Practice problems: 239. Sliding Window Maximum, 641. Design Circular Deque, 20. Valid Parentheses (can use deque).