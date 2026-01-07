# Queues

This section covers Queues in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a Queue?

A queue is a linear data structure that follows the First In, First Out (FIFO) principle. Elements are added at the rear and removed from the front.

## Implementation in Java

### Using Queue Interface with LinkedList
```java
import java.util.Queue;
import java.util.LinkedList;

Queue<Integer> queue = new LinkedList<>();
queue.add(1);      // Add to rear
queue.add(2);
int front = queue.peek();  // 1, without removing
int removed = queue.poll(); // 1, removes and returns
boolean empty = queue.isEmpty(); // false
int size = queue.size(); // 1
```

### Using Deque for more operations
```java
import java.util.Deque;
import java.util.ArrayDeque;

Deque<Integer> queue = new ArrayDeque<>();
queue.addLast(1);  // Add to rear
queue.addLast(2);
int front = queue.peekFirst();  // 1
int removed = queue.pollFirst(); // 1
```

## Basic Operations

- **add(element)** / **offer(element)**: Add element to rear. O(1)
- **poll()** / **remove()**: Remove and return front element. O(1)
- **peek()**: Return front element without removing. O(1)
- **isEmpty()**: Check if queue is empty. O(1)
- **size()**: Return number of elements. O(1)

## Common Problems and Solutions

### 1. Implement Queue using Stacks
```java
class MyQueue {
    private Deque<Integer> in;
    private Deque<Integer> out;

    public MyQueue() {
        in = new ArrayDeque<>();
        out = new ArrayDeque<>();
    }

    public void push(int x) {
        in.push(x);
    }

    public int pop() {
        if (out.isEmpty()) {
            while (!in.isEmpty()) {
                out.push(in.pop());
            }
        }
        return out.pop();
    }

    public int peek() {
        if (out.isEmpty()) {
            while (!in.isEmpty()) {
                out.push(in.pop());
            }
        }
        return out.peek();
    }

    public boolean empty() {
        return in.isEmpty() && out.isEmpty();
    }
}
```

### 2. Moving Average from Data Stream
```java
class MovingAverage {
    private Queue<Integer> queue;
    private int maxSize;
    private double sum;

    public MovingAverage(int size) {
        queue = new LinkedList<>();
        maxSize = size;
        sum = 0.0;
    }

    public double next(int val) {
        if (queue.size() == maxSize) {
            sum -= queue.poll();
        }
        queue.add(val);
        sum += val;
        return sum / queue.size();
    }
}
```

### 3. Number of Recent Calls
```java
class RecentCounter {
    private Queue<Integer> queue;

    public RecentCounter() {
        queue = new LinkedList<>();
    }

    public int ping(int t) {
        queue.add(t);
        while (queue.peek() < t - 3000) {
            queue.poll();
        }
        return queue.size();
    }
}
```

### 4. Binary Tree Level Order Traversal (using queue)
```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    while (!queue.isEmpty()) {
        int levelSize = queue.size();
        List<Integer> level = new ArrayList<>();
        for (int i = 0; i < levelSize; i++) {
            TreeNode node = queue.poll();
            level.add(node.val);
            if (node.left != null) queue.add(node.left);
            if (node.right != null) queue.add(node.right);
        }
        result.add(level);
    }
    return result;
}
```

## Time Complexities

- All operations: O(1)

## LeetCode Examples

### Problem: Implement Queue using Stacks
```java
// As above
```

### Problem: Moving Average from Data Stream
```java
// As above
```

### Problem: Number of Recent Calls
```java
// As above
```

## Tips for LeetCode
- Use LinkedList for Queue interface.
- For sliding window problems, use queue to maintain window.
- BFS often uses queues.
- Practice problems: 232. Implement Queue using Stacks, 346. Moving Average from Data Stream, 933. Number of Recent Calls, 102. Binary Tree Level Order Traversal.