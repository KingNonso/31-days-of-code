# Day 24: Dynamic Programming - Knapsack Pattern

## Overview

**Topic**: 0/1 Knapsack and subset sum problems
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Days 22-23 completed (1D and 2D DP)
- Understanding of DP recurrence relations
- Familiarity with subset problems

## Time Breakdown

- **Review (10 min)**: Review 2D DP patterns
- **Learn (40 min)**: Video + solve knapsack variation
- **Reflect (10 min)**: Document knapsack variations

## Resources

- [0/1 Knapsack Video](https://www.youtube.com/watch?v=8LusJS5-AGo) (20 min)
- [LeetCode 416 - Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

## Knapsack Problem Overview

**Classic 0/1 Knapsack:**

- Given items with weights and values
- Maximize value without exceeding capacity
- Each item can be used at most once (0/1)

**State**: `dp[i][w]` = max value using items 0..i with capacity w

**Recurrence**:

- If `weight[i] > w`: `dp[i][w] = dp[i-1][w]` (can't include)
- Else: `dp[i][w] = max(dp[i-1][w], dp[i-1][w-weight[i]] + value[i])`

## Tasks

### Task 1: Watch Knapsack Video (20 min)

Understand:

- 0/1 constraint: include or exclude each item
- How to build DP table
- Relationship to subset sum

### Task 2: Understand Knapsack Template (10 min)

```python
def knapsack(weights, values, capacity):
    n = len(weights)

    # dp[i][w] = max value using items 0..i-1 with capacity w
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            # Don't include item i-1
            dp[i][w] = dp[i-1][w]

            # Include item i-1 if it fits
            if weights[i-1] <= w:
                dp[i][w] = max(dp[i][w],
                               dp[i-1][w - weights[i-1]] + values[i-1])

    return dp[n][capacity]
```

### Task 3: Solve LeetCode 416 - Partition Equal Subset Sum (25 min)

- **Problem**: [LeetCode 416](https://leetcode.com/problems/partition-equal-subset-sum/)
- **Key Insight**: Can we find subset that sums to total/2?
- **Pattern**: This is 0/1 Knapsack where we check if target sum is achievable

```python
def canPartition(nums):
    total = sum(nums)

    # Can't partition odd sum
    if total % 2 != 0:
        return False

    target = total // 2

    # dp[i][s] = can we achieve sum s using items 0..i-1?
    # Simplified: dp[s] = can we achieve sum s?
    dp = [False] * (target + 1)
    dp[0] = True  # Sum 0 is always achievable

    for num in nums:
        # Traverse backwards to avoid using same item twice
        for s in range(target, num - 1, -1):
            dp[s] = dp[s] or dp[s - num]

    return dp[target]
```

**Why traverse backwards?**

- If we go forward, `dp[s - num]` might already use current `num`
- Going backward ensures we only use previous row's values

**Time Complexity**: O(n \* target)
**Space Complexity**: O(target)

### Task 4: Document Knapsack Variations (5 min)

**Knapsack Family:**

| Type         | Item Usage     | Example                 |
| ------------ | -------------- | ----------------------- |
| 0/1 Knapsack | Each item once | Subset sum, partition   |
| Unbounded    | Unlimited use  | Coin change (min coins) |
| Bounded      | Limited copies | Specific count per item |

**Recognizing Knapsack Problems:**

- "Partition into two groups"
- "Select subset with constraint"
- "Maximize/minimize with capacity"
- "Count ways to reach target"

**Related Problems:**

- Coin Change (unbounded)
- Target Sum (0/1 with +/-)
- Ones and Zeros (multi-dimensional)

## Output Requirements

What you must produce today:

- [ ] Accepted solution for LC 416
- [ ] Understanding of classic knapsack template
- [ ] Knapsack variations document

## Validation

How to verify you completed the work:

- Solution accepted
- Can explain backwards traversal
- Understand relationship to classic knapsack

## Success Criteria

- [ ] Understand 0/1 Knapsack pattern
- [ ] Know why backwards traversal is needed
- [ ] Can recognize knapsack problems
- [ ] Partition problem solved

## Common Pitfalls

- **Forward traversal**: Causes item reuse (wrong for 0/1)
- **Forgetting odd sum check**: Impossible to partition odd totals
- **Wrong target**: Target is total/2, not total
- **Not starting from 0**: `dp[0] = True` is base case

## Next Steps

Tomorrow you'll work on: **Day 25 - Graph BFS/DFS Basics** - Number of Islands, Clone Graph

## Social Post Template

"Day 24/31 DSA: Knapsack pattern = include or exclude. Partition problem is hidden knapsack! DP patterns repeating across problems. 🧠 #100DaysOfCode #Knapsack"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
