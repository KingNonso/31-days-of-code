# Day 3: Sliding Window - Fixed Size

## Overview

**Topic**: Fixed-size window for subarray/substring problems
**Estimated Time**: 60 minutes
**Difficulty**: Beginner-Intermediate

## Prerequisites

- Days 1-2 completed (two pointers patterns)
- Understanding of array traversal
- Basic math operations (sum, average)

## Time Breakdown

- **Review (10 min)**: Quick review of two-pointer patterns
- **Learn (40 min)**: Video + 2 problems with fixed window
- **Reflect (10 min)**: Write sliding window template code

## Resources

- [NeetCode Sliding Window](https://www.youtube.com/watch?v=jM2dhDPYMQM) (12 min)
- [LeetCode 643 - Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/)
- [LeetCode 1343 - Number of Subarrays of Size K](https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold/)

## Tasks

### Task 1: Watch Sliding Window Video (12 min)

Watch the NeetCode video focusing on:

- What defines a "window"
- How the window "slides" through the array
- Why this is O(n) instead of O(n\*k)

### Task 2: Solve LeetCode 643 - Maximum Average Subarray (18 min)

- **Problem**: [LeetCode 643](https://leetcode.com/problems/maximum-average-subarray-i/)
- **Pattern**: Fixed window of size k
- **Approach**:
  1. Calculate sum of first k elements
  2. Slide window: add next element, remove first element
  3. Track maximum sum seen
  4. Return max_sum / k
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

**Key Insight**: Don't recalculate entire sum each time. Just add new element and subtract old element.

### Task 3: Solve LeetCode 1343 - Subarrays Size K (18 min)

- **Problem**: [LeetCode 1343](https://leetcode.com/problems/number-of-sub-arrays-of-size-k-and-average-greater-than-or-equal-to-threshold/)
- **Pattern**: Fixed window with condition checking
- **Approach**:
  1. Calculate initial window sum
  2. Check if average >= threshold, increment count
  3. Slide window, check each new position
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

### Task 4: Write Sliding Window Template (12 min)

Create reusable template code:

```python
def fixed_sliding_window(arr, k):
    # Step 1: Initialize window with first k elements
    window_sum = sum(arr[:k])
    result = window_sum  # or process initial window

    # Step 2: Slide window from position k to end
    for i in range(k, len(arr)):
        # Add new element (entering window)
        window_sum += arr[i]
        # Remove old element (leaving window)
        window_sum -= arr[i - k]
        # Process/update result
        result = max(result, window_sum)

    return result
```

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 643, LC 1343)
- [ ] Fixed-size sliding window template code (saved)
- [ ] Written explanation: Why O(n) beats O(n\*k) brute force

## Validation

How to verify you completed the work:

- Both solutions pass all test cases
- Template code is syntactically correct
- Can trace through window movement step-by-step

## Success Criteria

- [ ] Understand the "add one, remove one" sliding technique
- [ ] Can identify fixed-window problems by keywords: "subarray of size k"
- [ ] Template code ready for future problems
- [ ] Time complexity improvement clearly understood

## Common Pitfalls

- **Recalculating window sum from scratch**: This defeats the purpose (O(n\*k))
- **Off-by-one in window boundaries**: Window indices: [i-k+1, i] or [i, i+k-1]
- **Integer overflow**: For large arrays, consider using long/float
- **Not handling k > array length**: Check edge case

## Next Steps

Tomorrow you'll work on: **Day 4 - Sliding Window (Variable Size)** - dynamic window expansion/contraction

## Social Post Template

"Day 3/31 DSA: Sliding window clicked! Fixed-size windows = O(n) vs O(n\*k) brute force. Template saved for future problems. #100DaysOfCode #LeetCode"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
