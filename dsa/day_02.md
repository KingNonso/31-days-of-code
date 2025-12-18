# Day 2: Two Pointers - Same Direction

## Overview

**Topic**: Fast & slow pointers for in-place array modification
**Estimated Time**: 60 minutes
**Difficulty**: Beginner

## Prerequisites

- Day 1 completed (opposite-end two pointers)
- Understanding of array indexing
- Familiarity with in-place modification concept

## Time Breakdown

- **Review (10 min)**: Revisit Day 1 solution and pattern notes
- **Learn (40 min)**: Solve 2 problems + compare approaches
- **Reflect (10 min)**: Document same-direction pattern and use cases

## Resources

- [LeetCode 26 - Remove Duplicates](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
- [LeetCode 27 - Remove Element](https://leetcode.com/problems/remove-element/)
- Day 1 pattern notes for comparison

## Tasks

### Task 1: Review Day 1 (5 min)

- Re-read your two-pointer pattern doc
- Recall the convergence logic from opposite-end pointers
- Consider: What if both pointers moved the same direction?

### Task 2: Solve LeetCode 26 - Remove Duplicates (15 min)

- **Problem**: [LeetCode 26](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
- **Pattern**: Slow pointer marks "write position," fast pointer scans
- **Approach**:
  1. Slow pointer stays at last unique element position
  2. Fast pointer finds next unique element
  3. Copy unique element to slow+1 position
- **Time Complexity**: O(n)
- **Space Complexity**: O(1) - in-place modification

### Task 3: Solve LeetCode 27 - Remove Element (15 min)

- **Problem**: [LeetCode 27](https://leetcode.com/problems/remove-element/)
- **Pattern**: Same slow/fast pointer approach
- **Approach**: Fast pointer skips unwanted values, slow pointer marks valid positions
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

### Task 4: Compare with Brute Force (15 min)

For each problem, consider the naive approach:

- **Brute force**: Create new array, copy valid elements → O(n) space
- **Two pointers**: Modify in-place → O(1) space

Write out both approaches and their complexities.

### Task 5: Document Pattern Comparison (10 min)

Create a comparison table:
| Aspect | Opposite-End | Same-Direction |
|--------|--------------|----------------|
| Use case | ? | ? |
| Pointer movement | ? | ? |
| Common problems | ? | ? |

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 26, LC 27)
- [ ] Comparison table: opposite-end vs same-direction use cases
- [ ] Written explanation of why same-direction achieves O(1) space

## Validation

How to verify you completed the work:

- Both solutions accepted with O(1) space complexity
- Can explain slow/fast pointer roles clearly
- Comparison table is complete and accurate

## Success Criteria

- [ ] Understand when to use slow/fast vs left/right pointers
- [ ] Can implement in-place array modification
- [ ] Recognize patterns: "modify in-place" → same-direction pointers
- [ ] Both problems solved optimally

## Common Pitfalls

- **Modifying array while iterating incorrectly**: Track positions carefully
- **Forgetting to return the new length**: These problems ask for length, not the array
- **Not handling empty arrays**: Check edge case of empty input
- **Confusing pointer roles**: Slow = write position, Fast = read position

## Next Steps

Tomorrow you'll work on: **Day 3 - Sliding Window (Fixed Size)** - subarray problems with constant window

## Social Post Template

"Day 2/31 DSA: Same-direction pointers = in-place array modification magic. Avoided O(n) extra space on 2 problems. Pattern library growing. #100DaysOfCode #DSA"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
