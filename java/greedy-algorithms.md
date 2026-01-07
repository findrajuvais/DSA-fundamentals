# Greedy Algorithms

This section covers Greedy Algorithms in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is Greedy?

Make locally optimal choice at each step, hoping for global optimum.

## Common Problems and Solutions

### 1. Jump Game
```java
public boolean canJump(int[] nums) {
    int farthest = 0;
    for (int i = 0; i < nums.length; i++) {
        if (i > farthest) return false;
        farthest = Math.max(farthest, i + nums[i]);
        if (farthest >= nums.length - 1) return true;
    }
    return true;
}
```

### 2. Jump Game II
```java
public int jump(int[] nums) {
    int jumps = 0, currentEnd = 0, farthest = 0;
    for (int i = 0; i < nums.length - 1; i++) {
        farthest = Math.max(farthest, i + nums[i]);
        if (i == currentEnd) {
            jumps++;
            currentEnd = farthest;
        }
    }
    return jumps;
}
```

### 3. Gas Station
```java
public int canCompleteCircuit(int[] gas, int[] cost) {
    int total = 0, tank = 0, start = 0;
    for (int i = 0; i < gas.length; i++) {
        int net = gas[i] - cost[i];
        tank += net;
        total += net;
        if (tank < 0) {
            start = i + 1;
            tank = 0;
        }
    }
    return total >= 0 ? start : -1;
}
```

### 4. Candy
```java
public int candy(int[] ratings) {
    int[] candies = new int[ratings.length];
    Arrays.fill(candies, 1);
    for (int i = 1; i < ratings.length; i++) {
        if (ratings[i] > ratings[i - 1]) {
            candies[i] = candies[i - 1] + 1;
        }
    }
    for (int i = ratings.length - 2; i >= 0; i--) {
        if (ratings[i] > ratings[i + 1]) {
            candies[i] = Math.max(candies[i], candies[i + 1] + 1);
        }
    }
    int total = 0;
    for (int c : candies) total += c;
    return total;
}
```

### 5. Task Scheduler
```java
public int leastInterval(char[] tasks, int n) {
    int[] freq = new int[26];
    for (char task : tasks) freq[task - 'A']++;
    Arrays.sort(freq);
    int maxFreq = freq[25];
    int idleTime = (maxFreq - 1) * n;
    for (int i = 24; i >= 0; i--) {
        idleTime -= Math.min(maxFreq - 1, freq[i]);
    }
    return idleTime > 0 ? idleTime + tasks.length : tasks.length;
}
```

## LeetCode Examples

### Problem: Jump Game
```java
// As above
```

### Problem: Gas Station
```java
// As above
```

## Tips for LeetCode
- Choose greedy choice that seems best at moment.
- Prove correctness if needed.
- Practice problems: 55. Jump Game, 45. Jump Game II, 134. Gas Station, 135. Candy, 621. Task Scheduler.