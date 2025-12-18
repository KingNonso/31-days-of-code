# Day 23: Dynamic Programming - 2D Problems

## Overview

**Topic**: 2D DP tables for grid and string problems
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate-Advanced

## Prerequisites

- Day 22 completed (1D DP)
- Understanding of DP recurrence relations
- Familiarity with 2D arrays

## Time Breakdown

- **Review (10 min)**: Review 1D DP patterns
- **Learn (40 min)**: Solve 2 2D DP problems
- **Reflect (10 min)**: Create 2D DP template

## Resources

- [LeetCode 62 - Unique Paths](https://leetcode.com/problems/unique-paths/)
- [LeetCode 1143 - Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

## When to Use 2D DP

- Grid traversal problems
- Two strings/sequences to compare
- When state depends on two variables

## Tasks

### Task 1: Review 1D DP (5 min)

Recall:

- Define state → Find recurrence → Base cases → Fill order → Optimize space
- 1D DP: state depends on one variable (position, amount, etc.)

### Task 2: Solve LeetCode 62 - Unique Paths (15 min)

- **Problem**: [LeetCode 62](https://leetcode.com/problems/unique-paths/)
- **Pattern**: Grid DP - count paths
- **State**: `dp[i][j]` = number of ways to reach cell (i, j)
- **Recurrence**: `dp[i][j] = dp[i-1][j] + dp[i][j-1]` (from top + from left)

```python
def uniquePaths(m, n):
    # dp[i][j] = ways to reach cell (i, j)
    dp = [[1] * n for _ in range(m)]

    # First row and column are all 1s (only one way to reach)
    # Already initialized

    for i in range(1, m):
        for j in range(1, n):
            dp[i][j] = dp[i-1][j] + dp[i][j-1]

    return dp[m-1][n-1]
```

**Space Optimized to O(n):**

```python
def uniquePaths(m, n):
    dp = [1] * n

    for i in range(1, m):
        for j in range(1, n):
            dp[j] = dp[j] + dp[j-1]

    return dp[n-1]
```

**Time Complexity**: O(m \* n)
**Space Complexity**: O(n) optimized

### Task 3: Solve LeetCode 1143 - Longest Common Subsequence (30 min)

- **Problem**: [LeetCode 1143](https://leetcode.com/problems/longest-common-subsequence/)
- **Pattern**: String DP - compare two sequences
- **State**: `dp[i][j]` = LCS length for text1[0:i] and text2[0:j]

**Recurrence:**

- If `text1[i-1] == text2[j-1]`: `dp[i][j] = dp[i-1][j-1] + 1`
- Else: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`

```python
def longestCommonSubsequence(text1, text2):
    m, n = len(text1), len(text2)

    # dp[i][j] = LCS of text1[0:i] and text2[0:j]
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    return dp[m][n]
```

**Understanding the DP table:**

```
    "" a c e
""   0 0 0 0
a    0 1 1 1
b    0 1 1 1
c    0 1 2 2
d    0 1 2 2
e    0 1 2 3

LCS of "abcde" and "ace" = 3 ("ace")
```

### Task 4: Create 2D DP Template (10 min)

**2D DP Template:**

```python
def solve_2d_dp(input1, input2):
    m, n = len(input1), len(input2)

    # Initialize DP table (often with extra row/col for base cases)
    dp = [[base_value] * (n + 1) for _ in range(m + 1)]

    # Fill base cases (first row, first column)
    # Often already handled by initialization

    # Fill DP table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            # Apply recurrence based on problem
            if condition:
                dp[i][j] = dp[i-1][j-1] + something
            else:
                dp[i][j] = combine(dp[i-1][j], dp[i][j-1])

    return dp[m][n]
```

**Key Patterns:**

- **Grid paths**: `dp[i][j] = dp[i-1][j] + dp[i][j-1]`
- **String matching**: Check if chars match, else take max of excluding one
- **Edit distance**: Similar to LCS with different operations

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 62, LC 1143)
- [ ] Hand-drawn DP table for LCS example
- [ ] 2D DP template documented

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can trace through DP table filling
- Understand space optimization technique

## Success Criteria

- [ ] Understand 2D DP table construction
- [ ] Can identify when 2D DP is needed
- [ ] Can trace through LCS table
- [ ] Both problems solved

## Common Pitfalls

- **Wrong indexing**: Off-by-one between string index and DP index
- **Wrong base case**: First row/column often need special handling
- **Wrong fill order**: Usually top-to-bottom, left-to-right
- **Not drawing the table**: Always visualize for string problems

## Next Steps

Tomorrow you'll work on: **Day 24 - DP: Knapsack Pattern** - 0/1 knapsack and partition problems

## Social Post Template

"Day 23/31 DSA: 2D DP = tables instead of arrays. LCS was tough but drawing the table made it click. Rows = string1, cols = string2. #100DaysOfCode #DP"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
