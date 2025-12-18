# Day 21: Week 3 Review - Advanced Patterns

## Overview

**Topic**: Consolidate backtracking, heap, and binary search with Top K problem
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate (Checkpoint)

## Prerequisites

- Days 15-20 completed
- All Week 3 patterns practiced
- Understanding of heaps and binary search

## Time Breakdown

- **Review (20 min)**: Review all Week 3 patterns
- **Learn (30 min)**: Solve Top K Frequent Elements
- **Reflect (10 min)**: Create complete pattern library

## Resources

- [LeetCode 347 - Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
- Your pattern docs from Days 15-20

## Patterns to Review

### Days 15-17: Backtracking

- **Template**: Make choice → Explore → Undo choice
- **Subsets**: Include/exclude each element
- **Combinations**: Subsets with size constraint
- **Permutations**: All orderings, use "used" array
- **Duplicates**: Sort + skip same values at same level

### Day 18: Heap / Priority Queue

- **Min-heap of size K** for Kth largest
- **Operations**: push O(log n), pop O(log n), peek O(1)
- **Pattern**: Opposite heap type, maintain size K

### Days 19-20: Binary Search

- **Template**: `while left <= right`, shrink search space
- **Rotated array**: One half always sorted
- **First/Last**: Save result, continue searching

## Tasks

### Task 1: Review All Week 3 Patterns (20 min)

For each pattern:

- Recall the template
- Remember 2-3 problems
- Note areas that need more practice

### Task 2: Solve LeetCode 347 - Top K Frequent (30 min)

- **Problem**: [LeetCode 347](https://leetcode.com/problems/top-k-frequent-elements/)
- **Pattern**: Hash map for frequency + heap for Top K
- **Multiple Approaches**: Heap, bucket sort, or quickselect

**Approach 1: Min-Heap (Recommended)**

```python
import heapq
from collections import Counter

def topKFrequent(nums, k):
    # Count frequencies
    freq = Counter(nums)

    # Use min-heap of size k
    # Store (frequency, element)
    heap = []

    for num, count in freq.items():
        heapq.heappush(heap, (count, num))
        if len(heap) > k:
            heapq.heappop(heap)

    return [num for count, num in heap]
```

**Time Complexity**: O(n log k)
**Space Complexity**: O(n) for frequency map

**Approach 2: Bucket Sort (O(n) time)**

```python
from collections import Counter

def topKFrequent(nums, k):
    freq = Counter(nums)

    # Bucket: index = frequency, value = list of elements
    buckets = [[] for _ in range(len(nums) + 1)]

    for num, count in freq.items():
        buckets[count].append(num)

    # Collect top k from highest buckets
    result = []
    for i in range(len(buckets) - 1, -1, -1):
        for num in buckets[i]:
            result.append(num)
            if len(result) == k:
                return result

    return result
```

**Time Complexity**: O(n)
**Space Complexity**: O(n)

### Task 3: Create Complete Pattern Library (10 min)

**Week 1-3 Pattern Summary:**

| Pattern        | Time            | Use When                      |
| -------------- | --------------- | ----------------------------- |
| Two Pointers   | O(n)            | Sorted array, palindrome      |
| Sliding Window | O(n)            | Contiguous subarray/substring |
| Hash Map       | O(n)            | Frequency, lookup             |
| Prefix Sum     | O(n) + O(1)     | Range queries                 |
| Recursion      | Varies          | Tree, divide & conquer        |
| BFS            | O(V+E)          | Level-order, shortest path    |
| DFS            | O(V+E)          | All paths, tree properties    |
| Backtracking   | O(2^n) or O(n!) | Generate all possibilities    |
| Heap           | O(n log k)      | Top K, Kth element            |
| Binary Search  | O(log n)        | Sorted array search           |

## Output Requirements

What you must produce today:

- [ ] Top K Frequent Elements solution accepted
- [ ] Complete pattern library (Weeks 1-3, ~15 patterns)
- [ ] Self-assessment: which patterns need more practice?

## Validation

How to verify you completed the work:

- Solution passes all test cases
- Pattern library is comprehensive
- Can recognize patterns in new problems

## Checkpoint Questions

1. What's the time complexity of backtracking for subsets? (O(2^n))
2. Why use min-heap for Top K largest? (Efficiently track K largest)
3. How do you find first occurrence with binary search? (Save result, search left)
4. How do you handle duplicates in permutations? (Sort + skip)
5. When is bucket sort O(n)? (When range is bounded)

## Success Criteria

- [ ] Top K problem solved with multiple approaches
- [ ] Can recognize when to use backtracking
- [ ] Can implement binary search bug-free
- [ ] Can use heaps for Top K problems

## Pattern Recognition Tips

- **"All possibilities"** → Backtracking
- **"Kth largest/smallest"** → Heap
- **"Find in sorted"** → Binary search
- **"Shortest path"** → BFS
- **"All paths"** → DFS
- **"Contiguous subarray"** → Sliding window
- **"Frequency counting"** → Hash map

## Next Steps

Tomorrow you'll work on: **Day 22 - Dynamic Programming: 1D Problems** - climbing stairs, house robber

## Social Post Template

"Week 3/31 DSA complete! Advanced patterns unlocked: backtracking for generation, heaps for Top K, binary search for O(log n). Pattern library = 15 strong. 🔥 #100DaysOfCode #DSA"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
