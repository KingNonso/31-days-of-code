# Day 20: Binary Search - Applications

## Overview

**Topic**: Binary search on rotated arrays and finding boundaries
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate-Advanced

## Prerequisites

- Day 19 completed (binary search template)
- Understanding of sorted arrays
- Strong grasp of binary search invariants

## Time Breakdown

- **Review (10 min)**: Review binary search template
- **Learn (40 min)**: Solve rotated array and boundary problems
- **Reflect (10 min)**: Document modified binary search patterns

## Resources

- [LeetCode 33 - Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- [LeetCode 34 - Find First and Last Position](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

## Tasks

### Task 1: Review Binary Search Template (5 min)

Recall the key elements:

- Loop condition: `while left <= right`
- Mid calculation: `mid = left + (right - left) // 2`
- Search space shrinks each iteration

### Task 2: Solve LeetCode 33 - Rotated Array Search (25 min)

- **Problem**: [LeetCode 33](https://leetcode.com/problems/search-in-rotated-sorted-array/)
- **Pattern**: Binary search with sorted half identification
- **Key Insight**: One half is always sorted!

```python
def search(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid

        # Check which half is sorted
        if nums[left] <= nums[mid]:
            # Left half is sorted
            if nums[left] <= target < nums[mid]:
                right = mid - 1  # Target in left half
            else:
                left = mid + 1   # Target in right half
        else:
            # Right half is sorted
            if nums[mid] < target <= nums[right]:
                left = mid + 1   # Target in right half
            else:
                right = mid - 1  # Target in left half

    return -1
```

**Why this works:**

1. Array is rotated, so one half is always sorted
2. Check if `nums[left] <= nums[mid]` to identify sorted half
3. If target is in sorted half, search there; otherwise, search other half

**Time Complexity**: O(log n)

### Task 3: Solve LeetCode 34 - First and Last Position (20 min)

- **Problem**: [LeetCode 34](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
- **Pattern**: Two binary searches - find left boundary, find right boundary

```python
def searchRange(nums, target):
    def findFirst(nums, target):
        left, right = 0, len(nums) - 1
        result = -1

        while left <= right:
            mid = left + (right - left) // 2

            if nums[mid] == target:
                result = mid
                right = mid - 1  # Keep searching left
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1

        return result

    def findLast(nums, target):
        left, right = 0, len(nums) - 1
        result = -1

        while left <= right:
            mid = left + (right - left) // 2

            if nums[mid] == target:
                result = mid
                left = mid + 1  # Keep searching right
            elif nums[mid] < target:
                left = mid + 1
            else:
                right = mid - 1

        return result

    return [findFirst(nums, target), findLast(nums, target)]
```

**Key insight:**

- To find FIRST: when found, save result and search LEFT
- To find LAST: when found, save result and search RIGHT

### Task 4: Document Binary Search Patterns (10 min)

**Binary Search Variants:**

| Variant          | When found, what next?        | Returns      |
| ---------------- | ----------------------------- | ------------ |
| Exact match      | Return immediately            | Index or -1  |
| First occurrence | Search left (right = mid - 1) | First index  |
| Last occurrence  | Search right (left = mid + 1) | Last index   |
| Insert position  | Return left when done         | Insert index |

**Pattern Recognition:**

- "Search in rotated array" → Identify sorted half, then binary search
- "Find first/last" → Two binary searches with different behaviors on match
- "Find insert position" → Standard binary search, return left

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 33, LC 34)
- [ ] Pattern doc: "Binary search variants: finding pivot, boundaries"
- [ ] Understanding of rotated array trick

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain "one half is always sorted" for rotated arrays
- Understand first vs last occurrence technique

## Success Criteria

- [ ] Can handle rotated sorted arrays
- [ ] Know how to find first/last occurrence
- [ ] Template adapts to different scenarios
- [ ] Both problems solved in O(log n)

## Common Pitfalls

- **Wrong half identification**: Use `nums[left] <= nums[mid]` (include equal)
- **Wrong boundary search**: First goes left on match, last goes right
- **Forgetting to save result**: Must save before continuing search
- **Not handling edge cases**: Empty array, single element

## Next Steps

Tomorrow you'll work on: **Day 21 - Week 3 Review** - backtracking + heap + binary search integration

## Social Post Template

"Day 20/31 DSA: Binary search on rotated arrays = identify sorted half, then search. First/last position = two binary searches. Template adapts! #100DaysOfCode #AlgorithmPatterns"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
