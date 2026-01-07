# Backtracking

This section covers Backtracking in Java for DSA, with syntax, methods, and examples to help solve LeetCode problems.

## What is Backtracking?

Try all possibilities, backtrack when invalid, find all solutions or optimal.

## Template
```java
public void backtrack(parameters) {
    if (base case) {
        // process solution
        return;
    }
    for (each choice) {
        // make choice
        backtrack(parameters);
        // undo choice
    }
}
```

## Common Problems and Solutions

### 1. Subsets
```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums, int start, List<Integer> path, List<List<Integer>> result) {
    result.add(new ArrayList<>(path));
    for (int i = start; i < nums.length; i++) {
        path.add(nums[i]);
        backtrack(nums, i + 1, path, result);
        path.remove(path.size() - 1);
    }
}
```

### 2. Permutations
```java
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums, List<Integer> path, List<List<Integer>> result) {
    if (path.size() == nums.length) {
        result.add(new ArrayList<>(path));
        return;
    }
    for (int num : nums) {
        if (path.contains(num)) continue;
        path.add(num);
        backtrack(nums, path, result);
        path.remove(path.size() - 1);
    }
}
```

### 3. Combination Sum
```java
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    List<List<Integer>> result = new ArrayList<>();
    Arrays.sort(candidates);
    backtrack(candidates, target, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] candidates, int target, int start, List<Integer> path, List<List<Integer>> result) {
    if (target == 0) {
        result.add(new ArrayList<>(path));
        return;
    }
    for (int i = start; i < candidates.length; i++) {
        if (candidates[i] > target) break;
        path.add(candidates[i]);
        backtrack(candidates, target - candidates[i], i, path, result);
        path.remove(path.size() - 1);
    }
}
```

### 4. N-Queens
```java
public List<List<String>> solveNQueens(int n) {
    List<List<String>> result = new ArrayList<>();
    char[][] board = new char[n][n];
    for (char[] row : board) Arrays.fill(row, '.');
    backtrack(board, 0, result);
    return result;
}

private void backtrack(char[][] board, int row, List<List<String>> result) {
    if (row == board.length) {
        result.add(construct(board));
        return;
    }
    for (int col = 0; col < board.length; col++) {
        if (isValid(board, row, col)) {
            board[row][col] = 'Q';
            backtrack(board, row + 1, result);
            board[row][col] = '.';
        }
    }
}

private boolean isValid(char[][] board, int row, int col) {
    for (int i = 0; i < row; i++) {
        if (board[i][col] == 'Q') return false;
        if (col - (row - i) >= 0 && board[i][col - (row - i)] == 'Q') return false;
        if (col + (row - i) < board.length && board[i][col + (row - i)] == 'Q') return false;
    }
    return true;
}

private List<String> construct(char[][] board) {
    List<String> path = new ArrayList<>();
    for (char[] row : board) path.add(new String(row));
    return path;
}
```

## LeetCode Examples

### Problem: Subsets
```java
// As above
```

### Problem: Permutations
```java
// As above
```

## Tips for LeetCode
- Use recursion with state tracking.
- Prune invalid paths early.
- For combinations, sort and skip duplicates.
- Practice problems: 78. Subsets, 46. Permutations, 39. Combination Sum, 51. N-Queens.