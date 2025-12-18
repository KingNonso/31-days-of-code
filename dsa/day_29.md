# Day 29: Mixed Practice - Medium Problems

## Overview

**Topic**: Apply pattern recognition to unfamiliar problems
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate-Advanced

## Prerequisites

- Weeks 1-4 completed
- All 20+ patterns practiced
- Strong pattern recognition skills

## Time Breakdown

- **Review (10 min)**: Quick pattern library review
- **Practice (40 min)**: Solve 2 mixed problems
- **Reflect (10 min)**: Document pattern recognition process

## Resources

- [LeetCode 875 - Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
- [LeetCode 49 - Group Anagrams](https://leetcode.com/problems/group-anagrams/)

## Tasks

### Task 1: Pattern Recognition Warm-up (10 min)

Before looking at problems, recall patterns by keyword:

- "Sorted array" → Binary search, Two pointers
- "Subarray/substring" → Sliding window
- "All possibilities" → Backtracking
- "Shortest path" → BFS/Dijkstra
- "Optimization" → DP
- "Grouping" → Hash map

### Task 2: Solve LeetCode 875 - Koko Eating Bananas (25 min)

- **Problem**: [LeetCode 875](https://leetcode.com/problems/koko-eating-bananas/)
- **Pattern Recognition**:
  - "Minimum speed" → Optimization
  - "Within h hours" → Constraint
  - Speed can be 1 to max(piles) → Search space!
- **Key Insight**: Binary search on the ANSWER SPACE (not the array!)

```python
import math

def minEatingSpeed(piles, h):
    # Binary search on speed k
    left, right = 1, max(piles)

    def canFinish(k):
        # Can Koko eat all piles in h hours at speed k?
        hours = sum(math.ceil(pile / k) for pile in piles)
        return hours <= h

    while left < right:
        mid = left + (right - left) // 2
        if canFinish(mid):
            right = mid  # Try smaller speed
        else:
            left = mid + 1  # Need faster speed

    return left
```

**Time Complexity**: O(n \* log(max(piles)))
**Space Complexity**: O(1)

**Why binary search on answer?**

- We're not searching in the array
- We're searching for the optimal speed (1 to max)
- If speed k works, any speed > k also works (monotonic)

### Task 3: Solve LeetCode 49 - Group Anagrams (15 min)

- **Problem**: [LeetCode 49](https://leetcode.com/problems/group-anagrams/)
- **Pattern Recognition**:
  - "Group by property" → Hash map
  - "Anagrams" → Same character counts
- **Key Insight**: Use sorted string or character count as key

```python
from collections import defaultdict

def groupAnagrams(strs):
    groups = defaultdict(list)

    for s in strs:
        # Key: sorted characters (anagrams have same sorted form)
        key = tuple(sorted(s))
        groups[key].append(s)

    return list(groups.values())
```

**Alternative with character count:**

```python
def groupAnagrams(strs):
    groups = defaultdict(list)

    for s in strs:
        # Key: character count tuple
        count = [0] * 26
        for c in s:
            count[ord(c) - ord('a')] += 1
        key = tuple(count)
        groups[key].append(s)

    return list(groups.values())
```

**Time Complexity**: O(n _ k) where k is max string length
**Space Complexity**: O(n _ k)

### Task 4: Document Pattern Recognition Process (10 min)

**My Pattern Recognition Process:**

1. **Read problem carefully**: Identify inputs, outputs, constraints
2. **Look for keywords**:
   - "Minimum/maximum" → DP or Binary Search
   - "All possibilities" → Backtracking
   - "Shortest" → BFS/Dijkstra
   - "Group/count" → Hash map
3. **Identify data structure**:
   - Sorted array → Binary search, Two pointers
   - Graph/grid → BFS/DFS
   - Tree → Recursion
4. **Check constraints**:
   - N ≤ 20 → Backtracking okay (2^20 ≈ 1M)
   - N ≤ 10^4 → O(n²) might work
   - N ≤ 10^6 → Need O(n) or O(n log n)
5. **Consider "search on answer"**:
   - If answer has a range and checking is easy
   - Binary search on the answer space

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 875, LC 49)
- [ ] Process doc: "How I identify the right pattern in 2-3 minutes"
- [ ] Understanding of binary search on answer space

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain pattern recognition for each
- Understand when to binary search on answer

## Success Criteria

- [ ] Solved unfamiliar problems using pattern recognition
- [ ] Understand binary search on answer space concept
- [ ] Pattern recognition process documented
- [ ] Both problems solved optimally

## Common Pitfalls

- **Jumping to code too fast**: Think pattern first
- **Missing binary search on answer**: Not just for arrays!
- **Overcomplicating**: Hash map is often enough for grouping
- **Wrong complexity analysis**: Check constraints first

## Next Steps

Tomorrow you'll work on: **Day 30 - Mock Interview Prep** - timed practice with communication

## Social Post Template

"Day 29/31 DSA: Koko Eating Bananas = binary search on ANSWER SPACE (not array). Mind = blown. Pattern recognition getting faster. #100DaysOfCode #MediumProblems"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
