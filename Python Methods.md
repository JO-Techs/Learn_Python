# Python Algorithmic Techniques

## 1. Recursion
### What?
A function that calls itself to solve smaller instances of the same problem. Requires a base case (stopping condition) and recursive case (self-call).

### Example (Factorial):
```python
def factorial(n):
    if n == 0:  # Base case
        return 1
    else:       # Recursive case
        return n * factorial(n - 1)
```

### Why Use?
- Natural for tree traversal, nested structures, or problems with self-similar subproblems (e.g., Fibonacci, directory traversal).

### Pros:
- Elegant, mirrors mathematical definitions.
- Simplifies complex problems (e.g., Tower of Hanoi).

### Cons:
- Risk of stack overflow for large inputs.
- Can be less efficient than iteration (Python lacks tail recursion optimization).

### Tips:
- Always define a clear base case first.
- Use for problems with subproblems of the same type (e.g., Fibonacci, tree traversals).

### Common Pitfalls:
- Forgetting the base case → infinite recursion.
- Redundant calculations (solve with memoization!).

---

## 2. Iteration (Loops)
### What?
Repeating operations using for/while loops.

### Example (Summing Numbers):
```python
total = 0
for num in range(1, 6):
    total += num
print(total)  # Output: 15
```

### Why Use?
- Direct control over repetition.
- Memory-efficient (no call stack overhead).

### Pros:
- Easy to debug and visualize.
- Efficient for linear tasks (e.g., array processing).

### Cons:
- Can get messy for nested or complex logic.

### Tips:
- Use `for` loops when the number of iterations is known.
- Use `while` for dynamic stopping conditions (e.g., user input).

### Common Pitfalls:
- Infinite loops (e.g., forgetting to update loop variables).

---

## 3. Divide and Conquer
### What?
Break a problem into smaller subproblems, solve them, and combine results.

### Example (Merge Sort):
```python
def merge_sort(arr):
    if len(arr) <= 1:  # Base case
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])  # Divide
    right = merge_sort(arr[mid:])
    return merge(left, right)     # Conquer & Combine
```

### Why Use?
- Efficient for large datasets (O(n log n) sorting, matrix multiplication).

### Pros:
- Parallelizable (subproblems are independent).
- Reduces problem complexity.

### Cons:
- Overhead of splitting/combining results.

### Tips:
- Ideal for sorting, matrix operations, or binary search.

### Common Pitfalls:
- Incorrect splitting logic → incomplete solutions.

---

## 4. Dynamic Programming (DP)
### What?
Optimize by reusing previous results. Two approaches:
- **Memoization:** Cache results (top-down).
- **Tabulation:** Build a table (bottom-up).

### Example (Fibonacci with Memoization):
```python
memo = {}
def fib(n):
    if n <= 1:
        return n
    if n not in memo:
        memo[n] = fib(n-1) + fib(n-2)  # Store result
    return memo[n]
```

### Why Use?
- Avoid redundant work in overlapping subproblems (e.g., shortest path, knapsack).

### Pros:
- Turns exponential time → polynomial time.

### Cons:
- Requires identifying optimal substructure.
- Extra memory for caching.

### Tips:
- Start with recursion, then add memoization.
- Use tabulation for space optimization.

### Common Pitfalls:
- Misidentifying subproblems → incorrect caching.

---

## 5. Backtracking
### What?
Explore all potential solutions incrementally, backtracking when a path fails.

### Example (N-Queens):
```python
def solve_n_queens(n):
    def backtrack(row, cols, diag, anti_diag, board):
        if row == n:  # Solution found
            solutions.append(["".join(row) for row in board])
            return
        for col in range(n):
            if col not in cols and row-col not in diag and row+col not in anti_diag:
                board[row][col] = 'Q'
                backtrack(row+1, cols|{col}, diag|{row-col}, anti_diag|{row+col}, board)
                board[row][col] = '.'  # Undo choice (backtrack)
    solutions = []
    backtrack(0, set(), set(), set(), [['.']*n for _ in range(n)])
    return solutions
```

### Why Use?
- Combinatorial problems (permutations, Sudoku, subset generation).

### Pros:
- Exhaustive search (guarantees a solution if it exists).

### Cons:
- Slow for large inputs (exponential time).

### Tips:
- Prune invalid paths early to save time.
- Use recursion + undo steps to explore possibilities.

### Common Pitfalls:
- Forgetting to reset state after backtracking → invalid solutions.

---

## How to Choose?
| Technique            | When to Use |
|----------------------|------------|
| **Recursion**       | Tree-like structures or when subproblems mirror the original. |
| **Iteration**       | Simple, linear tasks. |
| **Divide & Conquer**| Large datasets that can be split into independent parts. |
| **Dynamic Programming (DP)** | Overlapping subproblems (e.g., Fibonacci, grid traversal). |
| **Backtracking**    | Constraint-based combinatorial problems. |

### Practice Problems:
- Fibonacci (Recursion/DP)
- Merge Sort (Divide and Conquer)
- Sudoku Solver (Backtracking)
