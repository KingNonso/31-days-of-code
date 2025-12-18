# Day 17: Backtracking - Permutations

## Overview

**Topic**: Generating all orderings and handling duplicates
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate-Advanced

## Prerequisites

- Days 15-16 completed (backtracking, combinations)
- Understanding of backtracking template
- Familiarity with sorting

## Time Breakdown

- **Review (10 min)**: Review combination patterns
- **Learn (40 min)**: Solve Permutations and Permutations II
- **Reflect (10 min)**: Document duplicate-handling technique

## Resources

- [LeetCode 46 - Permutations](https://leetcode.com/problems/permutations/)
- [LeetCode 47 - Permutations II](https://leetcode.com/problems/permutations-ii/)

## Permutations vs Combinations

| Aspect               | Combinations | Permutations     |
| -------------------- | ------------ | ---------------- |
| Order matters?       | No           | Yes              |
| [1,2] vs [2,1]       | Same         | Different        |
| Use start index?     | Yes          | No (use visited) |
| Count for n elements | C(n,k)       | n!               |

## Tasks

### Task 1: Review Combinations (5 min)

Key difference for permutations:

- Order matters: [1,2,3] ≠ [3,2,1]
- We can use any unused element at each position
- Need to track which elements are used

### Task 2: Solve LeetCode 46 - Permutations (20 min)

- **Problem**: [LeetCode 46](https://leetcode.com/problems/permutations/)
- **Pattern**: Backtracking with "used" tracking
- **Time Complexity**: O(n! \* n)
- **Space Complexity**: O(n)

```python
def permute(nums):
    result = []
    used = [False] * len(nums)

    def backtrack(current):
        # Base case: permutation complete
        if len(current) == len(nums):
            result.append(current[:])
            return

        for i in range(len(nums)):
            if used[i]:
                continue

            # Make choice
            used[i] = True
            current.append(nums[i])

            # Explore
            backtrack(current)

            # Undo choice
            current.pop()
            used[i] = False

    backtrack([])
    return result
```

**Alternative without used array:**

```python
def permute(nums):
    result = []

    def backtrack(current, remaining):
        if not remaining:
            result.append(current[:])
            return

        for i in range(len(remaining)):
            current.append(remaining[i])
            backtrack(current, remaining[:i] + remaining[i+1:])
            current.pop()

    backtrack([], nums)
    return result
```

### Task 3: Solve LeetCode 47 - Permutations II (25 min)

- **Problem**: [LeetCode 47](https://leetcode.com/problems/permutations-ii/)
- **Pattern**: Backtracking with duplicate skipping
- **Key Insight**: Sort first, skip duplicates at same level

```python
def permuteUnique(nums):
    result = []
    nums.sort()  # Sort to group duplicates
    used = [False] * len(nums)

    def backtrack(current):
        if len(current) == len(nums):
            result.append(current[:])
            return

        for i in range(len(nums)):
            # Skip if already used
            if used[i]:
                continue

            # Skip duplicates at same level
            # If previous same value exists and wasn't used in this branch
            if i > 0 and nums[i] == nums[i-1] and not used[i-1]:
                continue

            used[i] = True
            current.append(nums[i])
            backtrack(current)
            current.pop()
            used[i] = False

    backtrack([])
    return result
```

**Why `not used[i-1]`?**

- If nums[i] == nums[i-1] and we haven't used nums[i-1] in current branch
- That means we're at same decision level and already explored with nums[i-1]
- So skip nums[i] to avoid duplicate permutation

### Task 4: Document Duplicate Handling (10 min)

**Duplicate Handling Strategy:**

1. **Sort the array first** - groups duplicates together
2. **Skip condition**: `nums[i] == nums[i-1] and not used[i-1]`
3. This ensures we only use first occurrence at each level

**Visualization for [1,1,2]:**

```
Without skip: generates [1,1,2] twice (once starting with each 1)
With skip: second 1 only used after first 1 is already in current
```

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 46, LC 47)
- [ ] Documentation: duplicate handling technique (sort + skip)
- [ ] Understanding why `not used[i-1]` prevents duplicates

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain the duplicate skipping logic
- Understand permutations vs combinations difference

## Success Criteria

- [ ] Can generate all permutations
- [ ] Know how to handle duplicates (sort + skip)
- [ ] Understand the skip condition deeply
- [ ] Both problems solved

## Common Pitfalls

- **Forgetting to sort**: Duplicate handling requires sorted array
- **Wrong skip condition**: `not used[i-1]` not `used[i-1]`
- **Using start index**: Permutations don't use start index (order matters)
- **Not resetting used**: Must set `used[i] = False` when backtracking

## Next Steps

Tomorrow you'll work on: **Day 18 - Heap / Priority Queue** - K-th largest and Top K problems

## Social Post Template

"Day 17/31 DSA: Permutations II taught me duplicate handling: sort first, skip duplicates at same level. Small trick, huge impact. #100DaysOfCode #Algorithms"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
