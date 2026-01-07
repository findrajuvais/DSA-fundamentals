# Graphs

This section covers Graphs in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is a Graph?

A graph consists of vertices (nodes) connected by edges. Can be directed/undirected, weighted/unweighted.

## Representation

### Adjacency List
```java
List<List<Integer>> adj = new ArrayList<>();
for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
adj.get(0).add(1);  // Edge 0 -> 1
```

### Adjacency Matrix
```java
int[][] matrix = new int[n][n];
matrix[0][1] = 1;  // Edge 0 -> 1
```

## Graph Traversals

### BFS (Breadth-First Search)
```java
public void bfs(int start, List<List<Integer>> adj) {
    boolean[] visited = new boolean[adj.size()];
    Queue<Integer> queue = new LinkedList<>();
    queue.add(start);
    visited[start] = true;
    while (!queue.isEmpty()) {
        int node = queue.poll();
        System.out.print(node + " ");
        for (int neighbor : adj.get(node)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.add(neighbor);
            }
        }
    }
}
```

### DFS (Depth-First Search)
```java
public void dfs(int node, List<List<Integer>> adj, boolean[] visited) {
    visited[node] = true;
    System.out.print(node + " ");
    for (int neighbor : adj.get(node)) {
        if (!visited[neighbor]) {
            dfs(neighbor, adj, visited);
        }
    }
}
```

## Common Problems and Solutions

### 1. Number of Islands
```java
public int numIslands(char[][] grid) {
    if (grid == null || grid.length == 0) return 0;
    int count = 0;
    for (int i = 0; i < grid.length; i++) {
        for (int j = 0; j < grid[0].length; j++) {
            if (grid[i][j] == '1') {
                count++;
                dfs(grid, i, j);
            }
        }
    }
    return count;
}

private void dfs(char[][] grid, int i, int j) {
    if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] == '0') return;
    grid[i][j] = '0';
    dfs(grid, i + 1, j);
    dfs(grid, i - 1, j);
    dfs(grid, i, j + 1);
    dfs(grid, i, j - 1);
}
```

### 2. Clone Graph
```java
class Node {
    public int val;
    public List<Node> neighbors;
    public Node(int _val) { val = _val; neighbors = new ArrayList<>(); }
}

public Node cloneGraph(Node node) {
    if (node == null) return null;
    Map<Node, Node> map = new HashMap<>();
    return dfs(node, map);
}

private Node dfs(Node node, Map<Node, Node> map) {
    if (map.containsKey(node)) return map.get(node);
    Node copy = new Node(node.val);
    map.put(node, copy);
    for (Node neighbor : node.neighbors) {
        copy.neighbors.add(dfs(neighbor, map));
    }
    return copy;
}
```

### 3. Course Schedule (Topological Sort)
```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    List<List<Integer>> adj = new ArrayList<>();
    int[] indegree = new int[numCourses];
    for (int i = 0; i < numCourses; i++) adj.add(new ArrayList<>());
    for (int[] pre : prerequisites) {
        adj.get(pre[1]).add(pre[0]);
        indegree[pre[0]]++;
    }
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < numCourses; i++) {
        if (indegree[i] == 0) queue.add(i);
    }
    int count = 0;
    while (!queue.isEmpty()) {
        int course = queue.poll();
        count++;
        for (int next : adj.get(course)) {
            indegree[next]--;
            if (indegree[next] == 0) queue.add(next);
        }
    }
    return count == numCourses;
}
```

### 4. Word Ladder
```java
public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    Set<String> wordSet = new HashSet<>(wordList);
    if (!wordSet.contains(endWord)) return 0;
    Queue<String> queue = new LinkedList<>();
    queue.add(beginWord);
    int level = 1;
    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            String word = queue.poll();
            if (word.equals(endWord)) return level;
            for (int j = 0; j < word.length(); j++) {
                char[] chars = word.toCharArray();
                for (char c = 'a'; c <= 'z'; c++) {
                    chars[j] = c;
                    String newWord = new String(chars);
                    if (wordSet.contains(newWord)) {
                        queue.add(newWord);
                        wordSet.remove(newWord);
                    }
                }
            }
        }
        level++;
    }
    return 0;
}
```

## Time Complexities

- BFS/DFS: O(V + E)
- Topological Sort: O(V + E)

## LeetCode Examples

### Problem: Number of Islands
```java
// As above
```

### Problem: Course Schedule
```java
// As above
```

## Tips for LeetCode
- Use adjacency list for sparse graphs.
- BFS for shortest path, DFS for connectivity.
- Topological sort for dependency problems.
- Practice problems: 200. Number of Islands, 133. Clone Graph, 207. Course Schedule, 127. Word Ladder.