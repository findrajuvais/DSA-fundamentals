# Binary Search Trees

This section covers Binary Search Trees (BST) in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a Binary Search Tree?

A BST is a binary tree where for each node, all elements in left subtree are less than node, and all in right are greater. This allows O(log n) operations.

## BST Node Implementation

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}
```

## Basic Operations

### Search
```java
public TreeNode search(TreeNode root, int val) {
    if (root == null || root.val == val) return root;
    if (val < root.val) return search(root.left, val);
    return search(root.right, val);
}
```

### Insert
```java
public TreeNode insert(TreeNode root, int val) {
    if (root == null) return new TreeNode(val);
    if (val < root.val) root.left = insert(root.left, val);
    else root.right = insert(root.right, val);
    return root;
}
```

### Delete
```java
public TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) return null;
    if (key < root.val) root.left = deleteNode(root.left, key);
    else if (key > root.val) root.right = deleteNode(root.right, key);
    else {
        if (root.left == null) return root.right;
        if (root.right == null) return root.left;
        TreeNode minNode = findMin(root.right);
        root.val = minNode.val;
        root.right = deleteNode(root.right, minNode.val);
    }
    return root;
}

private TreeNode findMin(TreeNode node) {
    while (node.left != null) node = node.left;
    return node;
}
```

### Validate BST
```java
public boolean isValidBST(TreeNode root) {
    return isValid(root, null, null);
}

private boolean isValid(TreeNode node, Integer min, Integer max) {
    if (node == null) return true;
    if ((min != null && node.val <= min) || (max != null && node.val >= max)) return false;
    return isValid(node.left, min, node.val) && isValid(node.right, node.val, max);
}
```

## Common Problems and Solutions

### 1. Kth Smallest Element in a BST
```java
public int kthSmallest(TreeNode root, int k) {
    Stack<TreeNode> stack = new Stack<>();
    TreeNode curr = root;
    int count = 0;
    while (curr != null || !stack.isEmpty()) {
        while (curr != null) {
            stack.push(curr);
            curr = curr.left;
        }
        curr = stack.pop();
        count++;
        if (count == k) return curr.val;
        curr = curr.right;
    }
    return -1;
}
```

### 2. Lowest Common Ancestor in BST
```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null) return null;
    if (p.val < root.val && q.val < root.val) return lowestCommonAncestor(root.left, p, q);
    if (p.val > root.val && q.val > root.val) return lowestCommonAncestor(root.right, p, q);
    return root;
}
```

### 3. Convert Sorted Array to BST
```java
public TreeNode sortedArrayToBST(int[] nums) {
    return build(nums, 0, nums.length - 1);
}

private TreeNode build(int[] nums, int start, int end) {
    if (start > end) return null;
    int mid = start + (end - start) / 2;
    TreeNode node = new TreeNode(nums[mid]);
    node.left = build(nums, start, mid - 1);
    node.right = build(nums, mid + 1, end);
    return node;
}
```

### 4. Range Sum of BST
```java
public int rangeSumBST(TreeNode root, int low, int high) {
    if (root == null) return 0;
    if (root.val < low) return rangeSumBST(root.right, low, high);
    if (root.val > high) return rangeSumBST(root.left, low, high);
    return root.val + rangeSumBST(root.left, low, high) + rangeSumBST(root.right, low, high);
}
```

## Time Complexities

- Search/Insert/Delete: O(log n) average, O(n) worst case
- Inorder traversal: O(n)

## LeetCode Examples

### Problem: Validate Binary Search Tree
```java
// As above
```

### Problem: Kth Smallest Element in a BST
```java
// As above
```

### Problem: Insert into a Binary Search Tree
```java
// As above, insert method
```

## Tips for LeetCode
- Use inorder traversal for sorted order.
- Recursive for simplicity, iterative for stack control.
- For LCA, use BST property to optimize.
- Practice problems: 98. Validate Binary Search Tree, 230. Kth Smallest Element in a BST, 235. Lowest Common Ancestor of a Binary Search Tree, 108. Convert Sorted Array to Binary Search Tree.