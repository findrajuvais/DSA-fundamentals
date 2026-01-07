# Graph Algorithms

This section covers Graph Algorithms in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## Shortest Path

### Dijkstra's Algorithm
```java
public int[] dijkstra(List<List<int[]>> graph, int start) {
    int n = graph.size();
    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[start] = 0;
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
    pq.add(new int[]{start, 0});
    while (!pq.isEmpty()) {
        int[] curr = pq.poll();
        int u = curr[0], d = curr[1];
        if (d > dist[u]) continue;
        for (int[] neighbor : graph.get(u)) {
            int v = neighbor[0], w = neighbor[1];
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.add(new int[]{v, dist[v]});
            }
        }
    }
    return dist;
}
```

### Bellman-Ford
```java
public int[] bellmanFord(List<List<int[]>> graph, int start, int n) {
    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[start] = 0;
    for (int i = 0; i < n - 1; i++) {
        for (int u = 0; u < n; u++) {
            if (dist[u] != Integer.MAX_VALUE) {
                for (int[] neighbor : graph.get(u)) {
                    int v = neighbor[0], w = neighbor[1];
                    if (dist[u] + w < dist[v]) {
                        dist[v] = dist[u] + w;
                    }
                }
            }
        }
    }
    // Check for negative cycles
    for (int u = 0; u < n; u++) {
        if (dist[u] != Integer.MAX_VALUE) {
            for (int[] neighbor : graph.get(u)) {
                int v = neighbor[0], w = neighbor[1];
                if (dist[u] + w < dist[v]) {
                    // Negative cycle
                }
            }
        }
    }
    return dist;
}
```

## Minimum Spanning Tree

### Kruskal's Algorithm
```java
public int kruskal(List<int[]> edges, int n) {
    Arrays.sort(edges, (a, b) -> a[2] - b[2]);
    int[] parent = new int[n];
    for (int i = 0; i < n; i++) parent[i] = i;
    int cost = 0;
    for (int[] edge : edges) {
        int u = edge[0], v = edge[1], w = edge[2];
        if (find(parent, u) != find(parent, v)) {
            union(parent, u, v);
            cost += w;
        }
    }
    return cost;
}

private int find(int[] parent, int i) {
    if (parent[i] != i) parent[i] = find(parent, parent[i]);
    return parent[i];
}

private void union(int[] parent, int i, int j) {
    parent[find(parent, i)] = find(parent, j);
}
```

### Prim's Algorithm
```java
public int prim(List<List<int[]>> graph, int n) {
    boolean[] visited = new boolean[n];
    int[] dist = new int[n];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[0] = 0;
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
    pq.add(new int[]{0, 0});
    int cost = 0;
    while (!pq.isEmpty()) {
        int[] curr = pq.poll();
        int u = curr[0];
        if (visited[u]) continue;
        visited[u] = true;
        cost += curr[1];
        for (int[] neighbor : graph.get(u)) {
            int v = neighbor[0], w = neighbor[1];
            if (!visited[v] && w < dist[v]) {
                dist[v] = w;
                pq.add(new int[]{v, w});
            }
        }
    }
    return cost;
}
```

## Other Algorithms

### Floyd-Warshall (All Pairs Shortest Path)
```java
public int[][] floydWarshall(int[][] graph) {
    int n = graph.length;
    int[][] dist = new int[n][n];
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            dist[i][j] = graph[i][j];
        }
    }
    for (int k = 0; k < n; k++) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (dist[i][k] != Integer.MAX_VALUE && dist[k][j] != Integer.MAX_VALUE) {
                    dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }
    }
    return dist;
}
```

## LeetCode Examples

### Problem: Network Delay Time (Dijkstra)
```java
public int networkDelayTime(int[][] times, int n, int k) {
    List<List<int[]>> graph = new ArrayList<>();
    for (int i = 0; i <= n; i++) graph.add(new ArrayList<>());
    for (int[] time : times) {
        graph.get(time[0]).add(new int[]{time[1], time[2]});
    }
    int[] dist = dijkstra(graph, k);
    int max = 0;
    for (int i = 1; i <= n; i++) {
        if (dist[i] == Integer.MAX_VALUE) return -1;
        max = Math.max(max, dist[i]);
    }
    return max;
}
```

### Problem: Find the City With the Smallest Number of Neighbors at a Threshold Distance (Floyd-Warshall)
```java
// Use floydWarshall
```

## Tips for LeetCode
- Use adjacency list for sparse graphs.
- PriorityQueue for Dijkstra.
- Union-Find for Kruskal.
- Practice problems: 743. Network Delay Time, 1584. Min Cost to Connect All Points, 1334. Find the City With the Smallest Number of Neighbors at a Threshold Distance.