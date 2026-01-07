# Linked Lists

This section covers Linked Lists in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a Linked List?

A linked list is a linear data structure where elements are stored in nodes, each containing data and a reference to the next node. In Java, we implement it using classes.

## Types of Linked Lists

- **Singly Linked List**: Each node points to the next.
- **Doubly Linked List**: Each node points to next and previous.
- **Circular Linked List**: Last node points back to first.

## Node Implementation

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

// For doubly
class DoublyListNode {
    int val;
    DoublyListNode next, prev;
    DoublyListNode(int x) { val = x; }
}
```

## Basic Operations

### Insertion
```java
// Insert at beginning
public ListNode insertAtHead(ListNode head, int val) {
    ListNode newNode = new ListNode(val);
    newNode.next = head;
    return newNode;
}

// Insert at end
public ListNode insertAtTail(ListNode head, int val) {
    if (head == null) return new ListNode(val);
    ListNode curr = head;
    while (curr.next != null) curr = curr.next;
    curr.next = new ListNode(val);
    return head;
}

// Insert after a node
public void insertAfter(ListNode prev, int val) {
    if (prev == null) return;
    ListNode newNode = new ListNode(val);
    newNode.next = prev.next;
    prev.next = newNode;
}
```

### Deletion
```java
// Delete node with value
public ListNode deleteNode(ListNode head, int val) {
    if (head == null) return null;
    if (head.val == val) return head.next;
    ListNode curr = head;
    while (curr.next != null && curr.next.val != val) {
        curr = curr.next;
    }
    if (curr.next != null) curr.next = curr.next.next;
    return head;
}

// Delete at position
public ListNode deleteAtPosition(ListNode head, int pos) {
    if (head == null) return null;
    if (pos == 0) return head.next;
    ListNode curr = head;
    for (int i = 0; curr != null && i < pos - 1; i++) {
        curr = curr.next;
    }
    if (curr == null || curr.next == null) return head;
    curr.next = curr.next.next;
    return head;
}
```

### Traversal
```java
public void printList(ListNode head) {
    ListNode curr = head;
    while (curr != null) {
        System.out.print(curr.val + " -> ");
        curr = curr.next;
    }
    System.out.println("null");
}
```

### Length
```java
public int getLength(ListNode head) {
    int len = 0;
    ListNode curr = head;
    while (curr != null) {
        len++;
        curr = curr.next;
    }
    return len;
}
```

## Common Problems and Solutions

### 1. Reverse Linked List
```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode curr = head;
    while (curr != null) {
        ListNode nextTemp = curr.next;
        curr.next = prev;
        prev = curr;
        curr = nextTemp;
    }
    return prev;
}
```

### 2. Detect Cycle (Floyd's Algorithm)
```java
public boolean hasCycle(ListNode head) {
    if (head == null) return false;
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;
    }
    return false;
}
```

### 3. Find Middle Node
```java
public ListNode middleNode(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```

### 4. Merge Two Sorted Lists
```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode curr = dummy;
    while (l1 != null && l2 != null) {
        if (l1.val < l2.val) {
            curr.next = l1;
            l1 = l1.next;
        } else {
            curr.next = l2;
            l2 = l2.next;
        }
        curr = curr.next;
    }
    curr.next = (l1 != null) ? l1 : l2;
    return dummy.next;
}
```

### 5. Remove Nth Node from End
```java
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode first = dummy, second = dummy;
    for (int i = 0; i <= n; i++) {
        first = first.next;
    }
    while (first != null) {
        first = first.next;
        second = second.next;
    }
    second.next = second.next.next;
    return dummy.next;
}
```

## Time Complexities

- Access: O(n)
- Insertion at head: O(1)
- Insertion at end: O(n)
- Deletion: O(n)
- Search: O(n)

## LeetCode Examples

### Problem: Reverse Linked List
```java
// Iterative solution above
// Recursive:
public ListNode reverseListRecursive(ListNode head) {
    if (head == null || head.next == null) return head;
    ListNode p = reverseListRecursive(head.next);
    head.next.next = head;
    head.next = null;
    return p;
}
```

### Problem: Linked List Cycle
```java
// As above, hasCycle
```

### Problem: Merge Two Sorted Lists
```java
// As above
```

## Tips for LeetCode
- Use dummy nodes for easier handling of head changes.
- Two pointers (slow/fast) for middle, cycle detection.
- Recursive solutions for reversal, but watch for stack overflow.
- Practice problems: 206. Reverse Linked List, 141. Linked List Cycle, 21. Merge Two Sorted Lists, 19. Remove Nth Node From End, 2. Add Two Numbers.