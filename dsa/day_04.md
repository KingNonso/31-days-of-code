# Day 4: Sliding Window - Variable Size

## Overview

**Topic**: Dynamic window expansion and contraction for optimization problems
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 3 completed (fixed-size sliding window)
- Understanding of hash maps/sets
- Familiarity with while loops and conditions

## Time Breakdown

- **Review (10 min)**: Review fixed-size template from Day 3
- **Learn (40 min)**: Solve 2 variable-window problems
- **Reflect (10 min)**: Document expand/contract decision logic

## Resources

- [LeetCode 3 - Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [LeetCode 209 - Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)
- Day 3 sliding window template for reference

## Tasks

### Task 1: Review Fixed-Size Template (5 min)

Recall the fixed window approach:

- Window size is constant
- We slide one position at a time

Now consider: What if optimal window size is unknown?

### Task 2: Solve LeetCode 3 - Longest Substring (25 min)

- **Problem**: [LeetCode 3](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- **Pattern**: Variable window - expand until invalid, contract until valid
- **Approach**:
  1. Use hash set to track characters in current window
  2. **Expand**: Add character to window (move right pointer)
  3. **Contract**: If duplicate found, remove from left until valid
  4. Track maximum window size
- **Time Complexity**: O(n) - each element visited at most twice
- **Space Complexity**: O(min(n, alphabet_size))

```python
def lengthOfLongestSubstring(s):
    char_set = set()
    left = 0
    max_length = 0

    for right in range(len(s)):
        # Contract: remove from left while duplicate exists
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        # Expand: add current character
        char_set.add(s[right])
        max_length = max(max_length, right - left + 1)

    return max_length
```

### Task 3: Solve LeetCode 209 - Minimum Size Subarray Sum (20 min)

- **Problem**: [LeetCode 209](https://leetcode.com/problems/minimum-size-subarray-sum/)
- **Pattern**: Variable window - expand until condition met, contract to minimize
- **Approach**:
  1. **Expand**: Add elements until sum >= target
  2. **Contract**: Shrink window while sum still >= target
  3. Track minimum window size
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

### Task 4: Create Decision Tree (10 min)

Document when to expand vs contract:

**Expand when:**

- Window doesn't meet condition yet
- Looking for longer/larger valid window

**Contract when:**

- Window exceeds constraint (e.g., duplicate found)
- Looking for shorter/smaller valid window
- Current window is valid, try to optimize

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 3, LC 209)
- [ ] Decision tree: when to expand vs contract window
- [ ] Comparison: fixed vs variable window patterns

## Validation

How to verify you completed the work:

- Both solutions accepted with optimal complexity
- Can explain the two-pointer movement in variable windows
- Decision tree clearly distinguishes expand/contract conditions

## Success Criteria

- [ ] Understand variable window expansion/contraction logic
- [ ] Can identify variable-window problems: "longest/shortest substring/subarray"
- [ ] Both problems solved optimally
- [ ] Can trace through algorithm step-by-step

## Common Pitfalls

- **Infinite loops**: Ensure left pointer doesn't exceed right
- **Wrong contraction condition**: Know when to stop shrinking
- **Using wrong data structure**: Hash set for uniqueness, hash map for counts
- **Not updating result at correct time**: Update after each valid state

## Next Steps

Tomorrow you'll work on: **Day 5 - Hash Maps** - frequency counting and O(1) lookups

## Social Post Template

"Day 4/31 DSA: Variable sliding windows are trickier but powerful. Key: define clear expand/contract conditions. Solved longest substring problem! #100DaysOfCode #CodeNewbie"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
