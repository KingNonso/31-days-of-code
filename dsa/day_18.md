# Day 18: Heap / Priority Queue

## Overview

**Topic**: K-th largest element, Top K problems using heaps
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Week 1-2 completed (arrays, trees)
- Understanding of complete binary trees
- Familiarity with Python's heapq (or equivalent)

## Time Breakdown

- **Review (10 min)**: Review backtracking patterns briefly
- **Learn (40 min)**: Video + solve 2 heap problems
- **Reflect (10 min)**: Document min-heap vs max-heap use cases

## Resources

- [Heap Data Structure Video](https://www.youtube.com/watch?v=HqPJF2L5h9U) (15 min)
- [LeetCode 215 - Kth Largest Element](https://leetcode.com/problems/kth-largest-element-in-an-array/)
- [LeetCode 703 - Kth Largest Element in Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)

## Heap Basics

**Heap Property:**

- **Min-Heap**: Parent ≤ children (smallest at root)
- **Max-Heap**: Parent ≥ children (largest at root)

**Operations:**
| Operation | Time Complexity |
|-----------|-----------------|
| Insert (push) | O(log n) |
| Extract min/max (pop) | O(log n) |
| Peek (get min/max) | O(1) |
| Build heap | O(n) |

**Python heapq** is a min-heap. For max-heap, negate values.

## Tasks

### Task 1: Learn Heap Operations (15 min)

Watch video and understand:

- Heap is a complete binary tree (array representation)
- Heapify up (after insert)
- Heapify down (after extract)

```python
import heapq

# Min-heap operations
heap = []
heapq.heappush(heap, 5)     # Insert
heapq.heappush(heap, 3)
heapq.heappush(heap, 7)
print(heap[0])              # Peek min: 3
min_val = heapq.heappop(heap)  # Extract min: 3

# Build heap from list
nums = [5, 3, 7, 1]
heapq.heapify(nums)         # O(n) - nums becomes heap
```

### Task 2: Solve LeetCode 215 - Kth Largest (20 min)

- **Problem**: [LeetCode 215](https://leetcode.com/problems/kth-largest-element-in-an-array/)
- **Pattern**: Min-heap of size K
- **Key Insight**: Keep smallest K elements → root is Kth largest

```python
import heapq

def findKthLargest(nums, k):
    # Use min-heap of size k
    heap = []

    for num in nums:
        heapq.heappush(heap, num)
        # If heap exceeds size k, remove smallest
        if len(heap) > k:
            heapq.heappop(heap)

    # Root is kth largest
    return heap[0]
```

**Time Complexity**: O(n log k)
**Space Complexity**: O(k)

**Why min-heap for Kth LARGEST?**

- We maintain k largest elements seen so far
- Min-heap lets us efficiently remove the smallest of these k
- After processing all elements, smallest of k largest = kth largest

**Alternative using nlargest:**

```python
import heapq

def findKthLargest(nums, k):
    return heapq.nlargest(k, nums)[-1]
```

### Task 3: Solve LeetCode 703 - Kth Largest in Stream (15 min)

- **Problem**: [LeetCode 703](https://leetcode.com/problems/kth-largest-element-in-a-stream/)
- **Pattern**: Maintain min-heap of size K across insertions

```python
import heapq

class KthLargest:
    def __init__(self, k, nums):
        self.k = k
        self.heap = nums
        heapq.heapify(self.heap)

        # Reduce to size k
        while len(self.heap) > k:
            heapq.heappop(self.heap)

    def add(self, val):
        heapq.heappush(self.heap, val)
        if len(self.heap) > self.k:
            heapq.heappop(self.heap)
        return self.heap[0]
```

### Task 4: Document Heap Use Cases (10 min)

**When to use Heaps:**

1. **Kth largest/smallest**: Min-heap of size K for Kth largest
2. **Top K elements**: Same pattern
3. **Merge K sorted lists**: Min-heap of K elements
4. **Continuous median**: Two heaps (max-heap + min-heap)
5. **Priority scheduling**: Process by priority

**Min-Heap vs Max-Heap:**

| Problem        | Use             |
| -------------- | --------------- |
| Kth largest    | Min-heap size K |
| Kth smallest   | Max-heap size K |
| Top K largest  | Min-heap size K |
| Top K smallest | Max-heap size K |

**Pattern**: Use OPPOSITE heap type, maintain size K

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 215, LC 703)
- [ ] Cheat sheet: "Use min-heap of size K for K-th largest"
- [ ] Understanding of heap operations and complexities

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain why min-heap for Kth largest
- Understand O(n log k) vs O(n log n) difference

## Success Criteria

- [ ] Understand heap data structure
- [ ] Can use heapq in Python (or equivalent)
- [ ] Know the "opposite heap, size K" pattern
- [ ] Both problems solved optimally

## Common Pitfalls

- **Using max-heap for Kth largest**: Use min-heap!
- **Not maintaining heap size**: Must pop when size > k
- **Forgetting heapify**: Use heapify for O(n) vs O(n log n) pushes
- **Python heapq is min-heap only**: Negate values for max-heap

## Next Steps

Tomorrow you'll work on: **Day 19 - Binary Search Templates** - avoiding off-by-one errors

## Social Post Template

"Day 18/31 DSA: Heaps = efficient priority management. Min-heap of size K tracks K largest elements. O(n log k) vs O(n log n). Smart! #100DaysOfCode #DataStructures"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
