# Day 22: Dynamic Programming - 1D Problems

## Overview

**Topic**: Introduction to DP with climbing stairs and house robber
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Week 3 completed (backtracking, heap, binary search)
- Strong recursion understanding
- Familiarity with memoization concept

## Time Breakdown

- **Review (10 min)**: Review recursion and memoization
- **Learn (40 min)**: Video + solve 2 DP problems
- **Reflect (10 min)**: Document DP decision framework

## Resources

- [NeetCode DP Intro](https://www.youtube.com/watch?v=oBt53YbR9Kk) (15 min)
- [LeetCode 70 - Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
- [LeetCode 198 - House Robber](https://leetcode.com/problems/house-robber/)

## What is Dynamic Programming?

**DP = Recursion + Memoization** (avoiding repeated work)

**When to use DP:**

1. **Optimal substructure**: Optimal solution uses optimal solutions to subproblems
2. **Overlapping subproblems**: Same subproblems are solved multiple times

## Tasks

### Task 1: Watch DP Intro Video (15 min)

Understand:

- Why recursion alone is inefficient (Fibonacci example)
- How memoization saves repeated work
- Top-down (memoization) vs Bottom-up (tabulation)

### Task 2: Solve LeetCode 70 - Climbing Stairs (15 min)

- **Problem**: [LeetCode 70](https://leetcode.com/problems/climbing-stairs/)
- **Key Insight**: This IS Fibonacci! `ways(n) = ways(n-1) + ways(n-2)`

**Approach 1: Top-Down (Memoization)**

```python
def climbStairs(n):
    memo = {}

    def dp(i):
        if i <= 2:
            return i
        if i in memo:
            return memo[i]
        memo[i] = dp(i-1) + dp(i-2)
        return memo[i]

    return dp(n)
```

**Approach 2: Bottom-Up (Tabulation)**

```python
def climbStairs(n):
    if n <= 2:
        return n

    dp = [0] * (n + 1)
    dp[1] = 1
    dp[2] = 2

    for i in range(3, n + 1):
        dp[i] = dp[i-1] + dp[i-2]

    return dp[n]
```

**Approach 3: Space Optimized**

```python
def climbStairs(n):
    if n <= 2:
        return n

    prev2, prev1 = 1, 2
    for i in range(3, n + 1):
        curr = prev1 + prev2
        prev2 = prev1
        prev1 = curr

    return prev1
```

**Time Complexity**: O(n) for all approaches
**Space Complexity**: O(n) for tabulation, O(1) for optimized

### Task 3: Solve LeetCode 198 - House Robber (20 min)

- **Problem**: [LeetCode 198](https://leetcode.com/problems/house-robber/)
- **Key Insight**: At each house, choose to rob (skip previous) or skip (take previous)
- **Recurrence**: `dp[i] = max(dp[i-1], dp[i-2] + nums[i])`

```python
def rob(nums):
    if len(nums) == 1:
        return nums[0]

    # dp[i] = max money robbing houses 0..i
    dp = [0] * len(nums)
    dp[0] = nums[0]
    dp[1] = max(nums[0], nums[1])

    for i in range(2, len(nums)):
        # Max of: skip this house, or rob this + best from i-2
        dp[i] = max(dp[i-1], dp[i-2] + nums[i])

    return dp[-1]
```

**Space Optimized:**

```python
def rob(nums):
    if len(nums) == 1:
        return nums[0]

    prev2 = nums[0]
    prev1 = max(nums[0], nums[1])

    for i in range(2, len(nums)):
        curr = max(prev1, prev2 + nums[i])
        prev2 = prev1
        prev1 = curr

    return prev1
```

### Task 4: Document DP Framework (10 min)

**DP Problem Solving Steps:**

1. **Define state**: What does `dp[i]` represent?
2. **Find recurrence**: How does `dp[i]` relate to previous states?
3. **Identify base cases**: What are the smallest subproblems?
4. **Determine order**: Which direction to fill the table?
5. **Optimize space**: Can we reduce from O(n) to O(1)?

**When to Use DP:**

- "Count the ways to..."
- "Minimum/maximum of..."
- "Is it possible to..."
- Problem has optimal substructure

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 70, LC 198)
- [ ] Both memoization and tabulation approaches for at least one
- [ ] DP decision framework document

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain recurrence relation for each
- Understand top-down vs bottom-up trade-offs

## Success Criteria

- [ ] Understand DP = recursion + memoization
- [ ] Can identify DP problems by keywords
- [ ] Can write both memoization and tabulation
- [ ] Both problems solved

## Common Pitfalls

- **Wrong base cases**: Carefully define edge cases
- **Wrong recurrence**: Draw out small examples first
- **Off-by-one in tabulation**: Check array indexing
- **Not considering all choices**: House robber has 2 choices per step

## Next Steps

Tomorrow you'll work on: **Day 23 - DP: 2D Problems** - unique paths, longest common subsequence

## Social Post Template

"Day 22/31 DSA: DP is recursion + memory. Climbing stairs = Fibonacci. House Robber = skip or take. Pattern: optimal substructure. #100DaysOfCode #DynamicProgramming"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
