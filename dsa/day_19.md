# Day 19: Binary Search - Templates

## Overview

**Topic**: Binary search on sorted arrays with off-by-one error prevention
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Week 1-2 completed
- Understanding of sorted arrays
- Familiarity with divide and conquer

## Time Breakdown

- **Review (10 min)**: Review heap patterns
- **Learn (40 min)**: Implement binary search + solve 2 problems
- **Reflect (10 min)**: Write bug-free binary search template

## Resources

- [LeetCode 704 - Binary Search](https://leetcode.com/problems/binary-search/)
- [LeetCode 35 - Search Insert Position](https://leetcode.com/problems/search-insert-position/)

## Binary Search Core Concept

**When to use**: Sorted array + search for target/position

**Key idea**: Eliminate half the search space each iteration

**Time Complexity**: O(log n)
**Space Complexity**: O(1) iterative, O(log n) recursive

## Tasks

### Task 1: Implement Binary Search from Scratch (15 min)

**Template (finding exact match):**

```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:  # Note: <= not <
        mid = left + (right - left) // 2  # Prevents overflow

        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1  # Not found
```

**Why `left + (right - left) // 2`?**

- `(left + right) // 2` can overflow for large values
- `left + (right - left) // 2` is always safe

**Why `left <= right`?**

- Search space is `[left, right]` inclusive
- Stop when search space is empty (`left > right`)

### Task 2: Solve LeetCode 704 - Binary Search (10 min)

- **Problem**: [LeetCode 704](https://leetcode.com/problems/binary-search/)
- **Pattern**: Standard binary search for exact match

```python
def search(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return -1
```

### Task 3: Solve LeetCode 35 - Search Insert Position (15 min)

- **Problem**: [LeetCode 35](https://leetcode.com/problems/search-insert-position/)
- **Pattern**: Binary search for insertion point
- **Key Insight**: When not found, `left` is the insertion point

```python
def searchInsert(nums, target):
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1

    return left  # Insertion point
```

**Why return left?**

- Loop ends when `left > right`
- At this point, `left` is where target should be inserted to maintain sorted order

### Task 4: Write Binary Search Template with Loop Invariant (10 min)

**Loop Invariant**: Answer is always in `[left, right]`

```python
def binary_search_template(nums, target):
    """
    Template for binary search.

    Loop invariant: If target exists, it's in [left, right]

    Returns: index of target, or -1 if not found
    """
    left, right = 0, len(nums) - 1

    while left <= right:
        mid = left + (right - left) // 2

        if nums[mid] == target:
            return mid  # Found
        elif nums[mid] < target:
            # Target in right half: [mid+1, right]
            left = mid + 1
        else:
            # Target in left half: [left, mid-1]
            right = mid - 1

    # Loop ended: left > right, target not found
    # left is the insertion point
    return -1  # or return left for insertion point
```

### Task 5: Test on Edge Cases (10 min)

Test your implementation:

- Empty array: `[]`
- Single element: `[5]`, target 5 and target 3
- Target at start: `[1,2,3,4,5]`, target 1
- Target at end: `[1,2,3,4,5]`, target 5
- Target not in array: `[1,3,5]`, target 2

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 704, LC 35)
- [ ] Binary search template with loop invariant documented
- [ ] Edge cases tested and passing

## Validation

How to verify you completed the work:

- Both solutions accepted
- Template handles all edge cases
- Can explain the loop invariant

## Success Criteria

- [ ] Can implement binary search bug-free
- [ ] Understand loop invariant concept
- [ ] Know why `left + (right - left) // 2` prevents overflow
- [ ] Template ready for variations

## Common Pitfalls

- **Off-by-one: `<` vs `<=`**: Use `<=` for `[left, right]` inclusive
- **Off-by-one: `mid` vs `mid+1`**: Be consistent with search space definition
- **Integer overflow**: Use `left + (right - left) // 2`
- **Infinite loop**: Ensure search space shrinks each iteration

## Next Steps

Tomorrow you'll work on: **Day 20 - Binary Search Applications** - rotated arrays and boundaries

## Social Post Template

"Day 19/31 DSA: Binary search is simple until you get off-by-one errors. Wrote a solid template with clear invariants. No more bugs! #100DaysOfCode #BinarySearch"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
