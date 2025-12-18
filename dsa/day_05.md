# Day 5: Hash Maps - Frequency Counting

## Overview

**Topic**: Using hash maps for O(1) lookups and frequency counting
**Estimated Time**: 60 minutes
**Difficulty**: Beginner-Intermediate

## Prerequisites

- Days 1-4 completed (two pointers, sliding window)
- Understanding of key-value pairs
- Familiarity with dictionary/hashmap in your language

## Time Breakdown

- **Review (10 min)**: Review sliding window problems that used sets/maps
- **Learn (40 min)**: Solve 3 hash map problems
- **Reflect (10 min)**: Document hash map patterns and use cases

## Resources

- [LeetCode 1 - Two Sum](https://leetcode.com/problems/two-sum/)
- [LeetCode 383 - Ransom Note](https://leetcode.com/problems/ransom-note/)
- [LeetCode 242 - Valid Anagram](https://leetcode.com/problems/valid-anagram/)

## Tasks

### Task 1: Solve LeetCode 1 - Two Sum (15 min)

- **Problem**: [LeetCode 1](https://leetcode.com/problems/two-sum/)
- **Pattern**: Hash map to remember seen elements
- **Approach**:
  1. For each number, calculate complement (target - num)
  2. Check if complement exists in hash map
  3. If yes, return indices; if no, add current to map
- **Time Complexity**: O(n) - single pass
- **Space Complexity**: O(n) - hash map storage

```python
def twoSum(nums, target):
    seen = {}  # value -> index
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []
```

**Key Insight**: Hash map turns O(n²) nested loop into O(n) single pass.

### Task 2: Solve LeetCode 383 - Ransom Note (15 min)

- **Problem**: [LeetCode 383](https://leetcode.com/problems/ransom-note/)
- **Pattern**: Frequency counting
- **Approach**:
  1. Count character frequencies in magazine
  2. For each char in ransom note, check if available
  3. Decrement count as characters are "used"
- **Time Complexity**: O(m + n)
- **Space Complexity**: O(1) - fixed alphabet size

### Task 3: Solve LeetCode 242 - Valid Anagram (15 min)

- **Problem**: [LeetCode 242](https://leetcode.com/problems/valid-anagram/)
- **Pattern**: Compare frequency counts
- **Approach**:
  1. Count frequencies in both strings
  2. Compare frequency maps
- **Time Complexity**: O(n)
- **Space Complexity**: O(1) - fixed alphabet

**Alternative**: Sort both strings and compare (O(n log n) time, O(1) space)

### Task 4: Document Hash Map Patterns (15 min)

Create pattern documentation:

**When to use Hash Maps:**

1. **Need O(1) lookup**: "Have we seen this before?"
2. **Frequency counting**: "How many times does X appear?"
3. **Two Sum variants**: "Find pair that sums to target"
4. **Grouping**: "Group items by some property"

**Hash Map vs Array:**
| Use Case | Hash Map | Array |
|----------|----------|-------|
| Keys are integers 0-n | ❌ | ✅ |
| Keys are arbitrary | ✅ | ❌ |
| Need O(1) lookup | ✅ | ✅ |
| Memory when keys sparse | ✅ | ❌ |

## Output Requirements

What you must produce today:

- [ ] 3 accepted solutions on LeetCode (LC 1, LC 383, LC 242)
- [ ] Pattern doc: "When hash maps beat arrays (with examples)"
- [ ] Template code for frequency counting

## Validation

How to verify you completed the work:

- All three solutions accepted
- Can explain O(1) lookup advantage
- Pattern doc includes concrete examples

## Success Criteria

- [ ] Understand hash map O(1) average lookup time
- [ ] Can implement frequency counting pattern
- [ ] Recognize "have we seen X?" → hash map
- [ ] All problems solved with optimal complexity

## Common Pitfalls

- **Using list instead of set/map**: O(n) lookup vs O(1)
- **Not handling missing keys**: Use `.get()` with default value
- **Hash collisions**: Usually handled by language, but be aware
- **Mutable keys**: Don't use lists as hash map keys

## Next Steps

Tomorrow you'll work on: **Day 6 - Prefix Sum** - cumulative sums for range queries

## Social Post Template

"Day 5/31 DSA: Hash maps = O(1) lookup superpower. Solved Two Sum in one pass. Pattern: need to 'remember' seen elements? Hash map. #100DaysOfCode #AlgorithmsMadeEasy"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
