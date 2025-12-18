# Day 16: Backtracking - Combinations

## Overview

**Topic**: Generating all valid combinations with backtracking
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate-Advanced

## Prerequisites

- Day 15 completed (backtracking fundamentals)
- Subsets problem understood
- Decision tree visualization skill

## Time Breakdown

- **Review (10 min)**: Review subsets solution and template
- **Learn (40 min)**: Solve Combinations and Combination Sum
- **Reflect (10 min)**: Compare subsets vs combinations vs permutations

## Resources

- [LeetCode 77 - Combinations](https://leetcode.com/problems/combinations/)
- [LeetCode 39 - Combination Sum](https://leetcode.com/problems/combination-sum/)

## Tasks

### Task 1: Review Subsets Pattern (5 min)

Recall the backtracking template:

1. Add choice to current state
2. Explore further
3. Remove choice (backtrack)

Key difference today: combinations have a **target size** or **target sum**.

### Task 2: Solve LeetCode 77 - Combinations (20 min)

- **Problem**: [LeetCode 77](https://leetcode.com/problems/combinations/)
- **Pattern**: Backtracking with size constraint
- **Difference from Subsets**: Only want combinations of exactly k elements

```python
def combine(n, k):
    result = []

    def backtrack(start, current):
        # Base case: found combination of size k
        if len(current) == k:
            result.append(current[:])
            return

        # Pruning: not enough elements left
        if len(current) + (n - start + 1) < k:
            return

        for i in range(start, n + 1):
            current.append(i)
            backtrack(i + 1, current)
            current.pop()

    backtrack(1, [])
    return result
```

**Time Complexity**: O(k \* C(n,k)) where C(n,k) is binomial coefficient
**Space Complexity**: O(k) for recursion

### Task 3: Solve LeetCode 39 - Combination Sum (25 min)

- **Problem**: [LeetCode 39](https://leetcode.com/problems/combination-sum/)
- **Pattern**: Backtracking with target sum, elements can be reused
- **Key Difference**: Same element can be used multiple times!

```python
def combinationSum(candidates, target):
    result = []

    def backtrack(start, current, remaining):
        # Base case: found valid combination
        if remaining == 0:
            result.append(current[:])
            return

        # Base case: exceeded target
        if remaining < 0:
            return

        for i in range(start, len(candidates)):
            current.append(candidates[i])
            # Note: i, not i+1, because we can reuse same element
            backtrack(i, current, remaining - candidates[i])
            current.pop()

    backtrack(0, [], target)
    return result
```

**Key insight**: `backtrack(i, ...)` allows reuse, `backtrack(i+1, ...)` prevents reuse.

### Task 4: Compare Patterns (10 min)

Create comparison document:

| Problem         | What we generate | Can reuse?             | When to add to result  |
| --------------- | ---------------- | ---------------------- | ---------------------- |
| Subsets         | All subsets      | No                     | Every node (or leaves) |
| Combinations    | Size k subsets   | No                     | When len == k          |
| Combination Sum | Sum = target     | Yes                    | When sum == target     |
| Permutations    | All orderings    | No (but order matters) | When len == n          |

**Key Parameters in Backtracking:**

1. **start index**: Prevents duplicates by only looking forward
2. **current state**: What we've built so far
3. **constraint**: When to stop (size, sum, etc.)

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 77, LC 39)
- [ ] Comparison doc: Subsets vs Combinations vs Permutations
- [ ] Understanding of when to use `i` vs `i+1` in recursion

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain difference between combination patterns
- Understand the "reuse" parameter in recursion

## Success Criteria

- [ ] Understand combinations = subsets with size constraint
- [ ] Know how to allow/prevent element reuse
- [ ] Can modify backtracking template for different constraints
- [ ] Both problems solved

## Common Pitfalls

- **Using i+1 when reuse allowed**: For Combination Sum, use `i`
- **Using i when reuse not allowed**: For Combinations, use `i+1`
- **Missing pruning**: Can skip early if impossible to reach target
- **Not copying current list**: Always use `current[:]`

## Next Steps

Tomorrow you'll work on: **Day 17 - Backtracking: Permutations** - generating all orderings

## Social Post Template

"Day 16/31 DSA: Combination Sum clicked when I drew the recursion tree. Same template, different constraints. Backtracking is powerful. #100DaysOfCode #LeetCode"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
