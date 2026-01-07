# Heaps

This section covers Heaps in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a Heap?

A heap is a complete binary tree that satisfies the heap property: in a max-heap, parent >= children; in min-heap, parent <= children. Used for priority queues.

## Implementation in Java

### Using PriorityQueue (Min-Heap by default)
```java
import java.util.PriorityQueue;

PriorityQueue<Integer> minHeap = new PriorityQueue<>();
minHeap.add(3);     // Add element
minHeap.add(1);
minHeap.add(2);
int min = minHeap.peek();  // 1
int removed = minHeap.poll(); // 1, removes and returns
boolean empty = minHeap.isEmpty();
int size = minHeap.size();
```

### Max-Heap
```java
PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a, b) -> b - a);
maxHeap.add(1);
maxHeap.add(3);
int max = maxHeap.peek();  // 3
```

## Basic Operations

- **add(element)** / **offer(element)**: Insert element. O(log n)
- **poll()**: Remove and return root. O(log n)
- **peek()**: Return root without removing. O(1)
- **isEmpty()**: Check if empty. O(1)
- **size()**: Return size. O(1)

## Common Problems and Solutions

### 1. Kth Largest Element in an Array
```java
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    for (int num : nums) {
        minHeap.add(num);
        if (minHeap.size() > k) minHeap.poll();
    }
    return minHeap.peek();
}
```

### 2. Top K Frequent Elements
```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> count = new HashMap<>();
    for (int num : nums) count.put(num, count.getOrDefault(num, 0) + 1);
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> b[1] - a[1]);
    for (Map.Entry<Integer, Integer> entry : count.entrySet()) {
        pq.add(new int[]{entry.getKey(), entry.getValue()});
    }
    int[] result = new int[k];
    for (int i = 0; i < k; i++) result[i] = pq.poll()[0];
    return result;
}
```

### 3. Merge K Sorted Lists
```java
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);
    for (ListNode list : lists) {
        if (list != null) pq.add(list);
    }
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    while (!pq.isEmpty()) {
        ListNode node = pq.poll();
        curr.next = node;
        curr = curr.next;
        if (node.next != null) pq.add(node.next);
    }
    return dummy.next;
}
```

### 4. Find Median from Data Stream
```java
class MedianFinder {
    private PriorityQueue<Integer> maxHeap; // left half
    private PriorityQueue<Integer> minHeap; // right half

    public MedianFinder() {
        maxHeap = new PriorityQueue<>((a, b) -> b - a);
        minHeap = new PriorityQueue<>();
    }

    public void addNum(int num) {
        maxHeap.add(num);
        minHeap.add(maxHeap.poll());
        if (maxHeap.size() < minHeap.size()) {
            maxHeap.add(minHeap.poll());
        }
    }

    public double findMedian() {
        if (maxHeap.size() > minHeap.size()) return maxHeap.peek();
        return (maxHeap.peek() + minHeap.peek()) / 2.0;
    }
}
```

## Time Complexities

- Insert: O(log n)
- Delete: O(log n)
- Peek: O(1)

## LeetCode Examples

### Problem: Kth Largest Element in an Array
```java
// As above
```

### Problem: Last Stone Weight
```java
public int lastStoneWeight(int[] stones) {
    PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> b - a);
    for (int stone : stones) pq.add(stone);
    while (pq.size() > 1) {
        int y = pq.poll();
        int x = pq.poll();
        if (x != y) pq.add(y - x);
    }
    return pq.isEmpty() ? 0 : pq.peek();
}
```

## Tips for LeetCode
- Use PriorityQueue for min/max heaps.
- For top K problems, maintain heap of size K.
- Two heaps for median problems.
- Practice problems: 215. Kth Largest Element in an Array, 347. Top K Frequent Elements, 23. Merge k Sorted Lists, 295. Find Median from Data Stream.