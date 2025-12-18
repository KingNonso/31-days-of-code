# Day 28: Week 4 Review - DP & Graph Integration

## Overview

**Topic**: Consolidate DP and Graph patterns with Coin Change
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate (Checkpoint)

## Prerequisites

- Days 22-27 completed
- All DP and graph patterns practiced
- Strong understanding of recurrence relations

## Time Breakdown

- **Review (20 min)**: Review all Week 4 patterns
- **Learn (30 min)**: Solve Coin Change problem
- **Reflect (10 min)**: Update master pattern library

## Resources

- [LeetCode 322 - Coin Change](https://leetcode.com/problems/coin-change/)
- Your pattern docs from Days 22-27

## Patterns to Review

### Days 22-24: Dynamic Programming

- **1D DP**: Climbing stairs, house robber
- **2D DP**: Unique paths, LCS
- **Knapsack**: 0/1, subset sum
- **Key**: State definition → Recurrence → Base cases

### Days 25-27: Graphs

- **BFS/DFS**: Islands, connected components
- **Dijkstra**: Weighted shortest path
- **Topological Sort**: Cycle detection, dependency ordering
- **Key**: Representation → Traversal → Visited tracking

## Tasks

### Task 1: Review All Week 4 Patterns (20 min)

For each pattern:

- Recall the template
- Remember 2-3 problems
- Note areas needing practice

### Task 2: Solve LeetCode 322 - Coin Change (30 min)

- **Problem**: [LeetCode 322](https://leetcode.com/problems/coin-change/)
- **Pattern**: Unbounded knapsack (can reuse coins)
- **This problem combines**: DP + optimization

**Approach 1: Bottom-Up DP**

```python
def coinChange(coins, amount):
    # dp[i] = min coins to make amount i
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0  # 0 coins for amount 0

    for i in range(1, amount + 1):
        for coin in coins:
            if coin <= i and dp[i - coin] != float('inf'):
                dp[i] = min(dp[i], dp[i - coin] + 1)

    return dp[amount] if dp[amount] != float('inf') else -1
```

**Approach 2: Top-Down with Memoization**

```python
def coinChange(coins, amount):
    memo = {}

    def dp(remaining):
        if remaining == 0:
            return 0
        if remaining < 0:
            return float('inf')
        if remaining in memo:
            return memo[remaining]

        min_coins = float('inf')
        for coin in coins:
            min_coins = min(min_coins, dp(remaining - coin) + 1)

        memo[remaining] = min_coins
        return min_coins

    result = dp(amount)
    return result if result != float('inf') else -1
```

**Time Complexity**: O(amount \* len(coins))
**Space Complexity**: O(amount)

**Why this is unbounded knapsack:**

- Same coin can be used multiple times
- We iterate through coins for EACH amount

### Task 3: Update Pattern Library (10 min)

**Complete Week 1-4 Pattern Summary:**

| Category      | Patterns                       | Key Problems                            |
| ------------- | ------------------------------ | --------------------------------------- |
| Arrays        | Two pointers, Sliding window   | Two Sum, 3Sum, Longest Substring        |
| Hash          | Frequency, Lookup              | Anagram, Two Sum                        |
| Trees         | BFS, DFS, Traversals           | Level Order, LCA, BST Validate          |
| Backtracking  | Subsets, Permutations          | Subsets, Combinations, Permutations     |
| Heap          | Top K, Kth element             | Kth Largest, Top K Frequent             |
| Binary Search | Exact, Boundary, Rotated       | Search Insert, Rotated Array            |
| DP            | 1D, 2D, Knapsack               | Climbing Stairs, LCS, Coin Change       |
| Graph         | BFS/DFS, Dijkstra, Topological | Islands, Network Delay, Course Schedule |

**Pattern Count: 20+**

## Output Requirements

What you must produce today:

- [ ] Coin Change solution accepted
- [ ] Complete pattern library (20+ patterns)
- [ ] Self-assessment of weak areas

## Validation

How to verify you completed the work:

- Solution passes all test cases
- Pattern library is comprehensive
- Can identify DP vs graph patterns

## Checkpoint Questions

1. What's the difference between 0/1 and unbounded knapsack? (Item reuse)
2. When do you use Dijkstra vs BFS? (Weighted vs unweighted)
3. How do you detect cycles in directed graphs? (3-state DFS)
4. What's the recurrence for coin change? (dp[i] = min(dp[i-coin] + 1))
5. What's the time complexity of topological sort? (O(V + E))

## Success Criteria

- [ ] Coin Change solved with both approaches
- [ ] Can identify DP problems by optimal substructure
- [ ] Can implement graph traversals from scratch
- [ ] Know which shortest path algorithm to use

## Week 4 Milestones Achieved

- [ ] Understand DP fundamentals (1D, 2D)
- [ ] Know knapsack variations (0/1, unbounded)
- [ ] Can traverse graphs with BFS/DFS
- [ ] Understand Dijkstra for weighted graphs
- [ ] Can perform topological sort

## Next Steps

Tomorrow you'll work on: **Day 29 - Mixed Practice** - applying multiple patterns

## Social Post Template

"Week 4/31 DSA done! DP demystified (just recursion + memo), graphs conquered (DFS/BFS/Dijkstra). Pattern library = 20+. Final stretch incoming! 💯 #100DaysOfCode #CodingProgress"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
