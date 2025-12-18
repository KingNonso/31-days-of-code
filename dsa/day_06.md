# Day 6: Prefix Sum

## Overview

**Topic**: Cumulative sums for efficient range queries
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Days 1-5 completed (two pointers, sliding window, hash maps)
- Understanding of array indexing
- Basic arithmetic operations

## Time Breakdown

- **Review (10 min)**: Review hash map patterns from Day 5
- **Learn (40 min)**: Solve 2 prefix sum problems
- **Reflect (10 min)**: Write prefix sum template and complexity analysis

## Resources

- [LeetCode 303 - Range Sum Query Immutable](https://leetcode.com/problems/range-sum-query-immutable/)
- [LeetCode 560 - Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

## Tasks

### Task 1: Understand Prefix Sum Concept (10 min)

**Prefix Sum Array**: `prefix[i]` = sum of all elements from index 0 to i

```
Original: [1, 2, 3, 4, 5]
Prefix:   [1, 3, 6, 10, 15]
```

**Key Formula**: Sum from index i to j = `prefix[j] - prefix[i-1]`

This turns O(n) range sum queries into O(1)!

### Task 2: Solve LeetCode 303 - Range Sum Query (20 min)

- **Problem**: [LeetCode 303](https://leetcode.com/problems/range-sum-query-immutable/)
- **Pattern**: Build prefix sum array, answer queries in O(1)
- **Approach**:
  1. In constructor: build prefix sum array
  2. In sumRange: return prefix[right] - prefix[left-1]
- **Time Complexity**: O(n) preprocessing, O(1) per query
- **Space Complexity**: O(n)

```python
class NumArray:
    def __init__(self, nums):
        self.prefix = [0] * (len(nums) + 1)
        for i in range(len(nums)):
            self.prefix[i + 1] = self.prefix[i] + nums[i]

    def sumRange(self, left, right):
        return self.prefix[right + 1] - self.prefix[left]
```

### Task 3: Solve LeetCode 560 - Subarray Sum Equals K (25 min)

- **Problem**: [LeetCode 560](https://leetcode.com/problems/subarray-sum-equals-k/)
- **Pattern**: Prefix sum + hash map (more challenging!)
- **Approach**:
  1. Track running prefix sum
  2. For each position, check if (prefix_sum - k) exists in map
  3. This means there's a subarray ending here that sums to k
- **Time Complexity**: O(n)
- **Space Complexity**: O(n)

```python
def subarraySum(nums, k):
    count = 0
    prefix_sum = 0
    prefix_counts = {0: 1}  # Base case: empty prefix

    for num in nums:
        prefix_sum += num
        # If (prefix_sum - k) was seen before, those subarrays sum to k
        if prefix_sum - k in prefix_counts:
            count += prefix_counts[prefix_sum - k]
        # Record this prefix sum
        prefix_counts[prefix_sum] = prefix_counts.get(prefix_sum, 0) + 1

    return count
```

**Key Insight**: If `prefix[j] - prefix[i] = k`, then subarray from i+1 to j sums to k.

### Task 4: Write Template and Analysis (5 min)

Document:

- Prefix sum template code
- When to use: multiple range queries on static array
- Complexity comparison: brute force O(n) per query vs prefix sum O(1) per query

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 303, LC 560)
- [ ] Prefix sum template code with comments
- [ ] Complexity analysis: prefix sum vs brute force for range queries

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain the prefix[j] - prefix[i-1] formula
- Understand LC 560's combination of prefix sum + hash map

## Success Criteria

- [ ] Understand prefix sum array construction
- [ ] Can answer range sum queries in O(1)
- [ ] Understand the hash map optimization for "subarray sum = k"
- [ ] Both problems solved optimally

## Common Pitfalls

- **Off-by-one errors**: Be careful with prefix array indexing
- **Forgetting base case in LC 560**: Initialize with {0: 1}
- **Not handling negative numbers**: LC 560 works with negatives too
- **Confusing prefix sum with running sum**: They're related but different patterns

## Next Steps

Tomorrow you'll work on: **Day 7 - Week 1 Review & Checkpoint** - consolidate all patterns with 3Sum

## Social Post Template

"Day 6/31 DSA: Prefix sums turn O(n) range queries into O(1). Mind blown by the cumulative sum trick. #100DaysOfCode #DataStructures"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
