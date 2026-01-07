# Trees

This section covers Trees in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a Tree?

A tree is a hierarchical data structure with a root node and child nodes. Each node has at most two children in a binary tree.

## Tree Node Implementation

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}
```

## Tree Traversals

### Inorder (Left, Root, Right)
```java
public void inorder(TreeNode root) {
    if (root == null) return;
    inorder(root.left);
    System.out.print(root.val + " ");
    inorder(root.right);
}
```

### Preorder (Root, Left, Right)
```java
public void preorder(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val + " ");
    preorder(root.left);
    preorder(root.right);
}
```

### Postorder (Left, Right, Root)
```java
public void postorder(TreeNode root) {
    if (root == null) return;
    postorder(root.left);
    postorder(root.right);
    System.out.print(root.val + " ");
}
```

### Level Order (BFS)
```java
public void levelOrder(TreeNode root) {
    if (root == null) return;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.add(root);
    while (!queue.isEmpty()) {
        TreeNode node = queue.poll();
        System.out.print(node.val + " ");
        if (node.left != null) queue.add(node.left);
        if (node.right != null) queue.add(node.right);
    }
}
```

## Common Problems and Solutions

### 1. Maximum Depth of Binary Tree
```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    int left = maxDepth(root.left);
    int right = maxDepth(root.right);
    return Math.max(left, right) + 1;
}
```

### 2. Same Tree
```java
public boolean isSameTree(TreeNode p, TreeNode q) {
    if (p == null && q == null) return true;
    if (p == null || q == null) return false;
    return p.val == q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
}
```

### 3. Invert Binary Tree
```java
public TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    TreeNode temp = root.left;
    root.left = root.right;
    root.right = temp;
    invertTree(root.left);
    invertTree(root.right);
    return root;
}
```

### 4. Binary Tree Paths
```java
public List<String> binaryTreePaths(TreeNode root) {
    List<String> paths = new ArrayList<>();
    if (root == null) return paths;
    dfs(root, "", paths);
    return paths;
}

private void dfs(TreeNode node, String path, List<String> paths) {
    path += node.val;
    if (node.left == null && node.right == null) {
        paths.add(path);
        return;
    }
    if (node.left != null) dfs(node.left, path + "->", paths);
    if (node.right != null) dfs(node.right, path + "->", paths);
}
```

### 5. Lowest Common Ancestor
```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    if (left != null && right != null) return root;
    return left != null ? left : right;
}
```

## Time Complexities

- Traversal: O(n)
- Search/Insert/Delete: O(n) for unbalanced, O(log n) for balanced

## LeetCode Examples

### Problem: Maximum Depth of Binary Tree
```java
// As above
```

### Problem: Symmetric Tree
```java
public boolean isSymmetric(TreeNode root) {
    return isMirror(root, root);
}

private boolean isMirror(TreeNode t1, TreeNode t2) {
    if (t1 == null && t2 == null) return true;
    if (t1 == null || t2 == null) return false;
    return t1.val == t2.val && isMirror(t1.left, t2.right) && isMirror(t1.right, t2.left);
}
```

## Tips for LeetCode
- Use recursion for tree problems.
- BFS for level order, DFS for path finding.
- Check for null nodes.
- Practice problems: 104. Maximum Depth of Binary Tree, 100. Same Tree, 226. Invert Binary Tree, 257. Binary Tree Paths, 236. Lowest Common Ancestor of a Binary Tree.