# Day 7: Week 1 Review & Checkpoint

## Overview

**Topic**: Consolidate Week 1 patterns with a medium difficulty problem
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate (Checkpoint)

## Prerequisites

- Days 1-6 completed
- All 6 pattern documents created
- At least 12 problems solved this week

## Time Breakdown

- **Review (15 min)**: Review all 6 pattern docs from this week
- **Learn (35 min)**: Solve 3Sum combining multiple patterns
- **Reflect (10 min)**: Create Week 1 cheat sheet

## Resources

- [LeetCode 15 - 3Sum](https://leetcode.com/problems/3sum/)
- Your pattern docs from Days 1-6
- [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) (optional advanced)

## Patterns to Review

### Pattern 1: Two Pointers - Opposite Ends (Day 1)

- Use: Sorted arrays, palindromes
- Key: Left and right pointers converging

### Pattern 2: Two Pointers - Same Direction (Day 2)

- Use: In-place modification
- Key: Slow (write) and fast (read) pointers

### Pattern 3: Sliding Window - Fixed (Day 3)

- Use: Subarrays of size k
- Key: Add new, remove old in O(1)

### Pattern 4: Sliding Window - Variable (Day 4)

- Use: Longest/shortest substring/subarray
- Key: Expand until invalid, contract until valid

### Pattern 5: Hash Maps (Day 5)

- Use: O(1) lookup, frequency counting
- Key: "Have we seen this before?"

### Pattern 6: Prefix Sum (Day 6)

- Use: Range queries, subarray sums
- Key: prefix[j] - prefix[i-1] = sum(i to j)

## Tasks

### Task 1: Review All Patterns (15 min)

Go through each pattern doc and:

- Recall the template code
- Remember at least 2 problems for each
- Note any patterns that feel weak

### Task 2: Solve LeetCode 15 - 3Sum (35 min)

- **Problem**: [LeetCode 15](https://leetcode.com/problems/3sum/)
- **Why this problem**: Combines sorting + two pointers + duplicate handling
- **Approach**:
  1. **Sort the array** (enables two pointers)
  2. For each element i, use **two pointers** to find pairs that sum to -nums[i]
  3. **Skip duplicates** to avoid duplicate triplets
- **Time Complexity**: O(n²) - can't do better for this problem
- **Space Complexity**: O(1) excluding output

```python
def threeSum(nums):
    nums.sort()
    result = []

    for i in range(len(nums) - 2):
        # Skip duplicates for first element
        if i > 0 and nums[i] == nums[i-1]:
            continue

        # Two pointers for remaining two elements
        left, right = i + 1, len(nums) - 1
        target = -nums[i]

        while left < right:
            current_sum = nums[left] + nums[right]
            if current_sum == target:
                result.append([nums[i], nums[left], nums[right]])
                # Skip duplicates
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                left += 1
                right -= 1
            elif current_sum < target:
                left += 1
            else:
                right -= 1

    return result
```

### Task 3: Create Week 1 Cheat Sheet (10 min)

Create a 1-page reference with:

- All 6 patterns with one-line descriptions
- When to use each pattern (keywords to look for)
- Time complexity for each
- One example problem per pattern

## Output Requirements

What you must produce today:

- [ ] 3Sum solution accepted on LeetCode
- [ ] 1-page cheat sheet with all Week 1 patterns
- [ ] Self-assessment: which patterns need more practice?

## Validation

How to verify you completed the work:

- 3Sum passes all test cases including edge cases
- Cheat sheet covers all 6 patterns
- Can identify which pattern applies to a new problem in < 2 minutes

## Success Criteria

- [ ] Solved medium problem (3Sum) combining patterns
- [ ] Can explain why sorting enables the two-pointer approach
- [ ] Understand duplicate handling in 3Sum
- [ ] All patterns documented and accessible

## Checkpoint Questions

Answer these to validate your Week 1 learning:

1. What's the time complexity of brute force 3Sum? (O(n³))
2. How does sorting help reduce complexity? (Enables two pointers → O(n²))
3. Which pattern finds pairs summing to target in sorted array? (Two pointers - opposite ends)
4. When do you use variable vs fixed sliding window? (Unknown vs known window size)
5. What data structure gives O(1) lookup? (Hash map/set)

## Common Pitfalls

- **Not sorting first**: Two pointers requires sorted array
- **Missing duplicates**: Skip duplicate values at all levels
- **Wrong pointer movement**: Move toward center based on sum comparison
- **Edge cases**: Empty array, all zeros, no solution

## Next Steps

Tomorrow you'll work on: **Day 8 - Recursion Basics** - recursive thinking and base cases

## Social Post Template

"Week 1/31 DSA complete! Mastered 6 core patterns: two pointers, sliding window, hash maps, prefix sum. First medium problem solved using multiple patterns. Momentum building. 🚀 #100DaysOfCode #CodingJourney"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
