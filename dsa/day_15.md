# Day 15: Backtracking - Fundamentals

## Overview

**Topic**: Explore all possibilities with decision trees and pruning
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate-Advanced

## Prerequisites

- Week 2 completed (recursion, trees)
- Strong understanding of recursion
- Familiarity with decision trees

## Time Breakdown

- **Review (10 min)**: Review recursion patterns
- **Learn (40 min)**: Video + solve Subsets with decision tree
- **Reflect (10 min)**: Create backtracking template

## Resources

- [NeetCode Backtracking Intro](https://www.youtube.com/watch?v=pfiQ_PS1g8E) (18 min)
- [LeetCode 78 - Subsets](https://leetcode.com/problems/subsets/)

## What is Backtracking?

Backtracking = DFS + undo (backtrack)

**Core idea**: Explore all possibilities by:

1. Making a choice
2. Exploring further with that choice
3. Undoing the choice (backtrack)
4. Try the next choice

## Tasks

### Task 1: Watch Backtracking Video (18 min)

Focus on:

- Decision tree visualization
- "Include or exclude" pattern
- How backtracking differs from regular recursion

### Task 2: Solve LeetCode 78 - Subsets (30 min)

- **Problem**: [LeetCode 78](https://leetcode.com/problems/subsets/)
- **Pattern**: Include/exclude each element
- **Time Complexity**: O(2^n) - we generate 2^n subsets
- **Space Complexity**: O(n) - recursion depth

**Approach 1: Include/Exclude Decision**

```python
def subsets(nums):
    result = []

    def backtrack(index, current):
        # Base case: processed all elements
        if index == len(nums):
            result.append(current[:])  # Copy current subset
            return

        # Choice 1: Include nums[index]
        current.append(nums[index])
        backtrack(index + 1, current)

        # Choice 2: Exclude nums[index] (backtrack)
        current.pop()
        backtrack(index + 1, current)

    backtrack(0, [])
    return result
```

**Approach 2: Iterative Building**

```python
def subsets(nums):
    result = []

    def backtrack(start, current):
        result.append(current[:])  # Add current subset

        for i in range(start, len(nums)):
            current.append(nums[i])
            backtrack(i + 1, current)
            current.pop()  # Backtrack

    backtrack(0, [])
    return result
```

### Task 3: Draw Decision Tree for subsets([1,2,3]) (12 min)

Visualize the choices:

```
                    []
                  /    \
            [1]          []
           /   \        /   \
       [1,2]  [1]    [2]    []
       /  \   / \    / \    / \
   [1,2,3][1,2][1,3][1][2,3][2][3][]
```

Each path from root to leaf is a subset!

**Key Observations:**

- Binary tree: each element has include/exclude choice
- 2^n leaves = 2^n subsets
- Backtracking = going back up the tree

## Output Requirements

What you must produce today:

- [ ] Accepted solution for LeetCode 78
- [ ] Hand-drawn decision tree for subsets([1,2,3])
- [ ] Backtracking template with add/explore/remove pattern

## Backtracking Template

```python
def backtrack(state, choices):
    if is_solution(state):
        result.append(state[:])  # Save copy
        return

    for choice in choices:
        if is_valid(choice):
            # 1. Make choice
            state.append(choice)

            # 2. Explore
            backtrack(state, next_choices)

            # 3. Undo choice (backtrack)
            state.pop()
```

## Validation

How to verify you completed the work:

- Solution generates all 2^n subsets
- Decision tree shows all paths
- Can trace through backtracking step by step

## Success Criteria

- [ ] Understand backtracking = DFS + undo
- [ ] Can draw decision trees for backtracking problems
- [ ] Template memorized: add → explore → remove
- [ ] Subsets problem solved optimally

## Common Pitfalls

- **Forgetting to copy**: `result.append(current[:])` not `result.append(current)`
- **Not backtracking**: Must undo choice after exploring
- **Wrong base case**: Know when to stop recursing
- **Modifying during iteration**: Be careful with loop indices

## Next Steps

Tomorrow you'll work on: **Day 16 - Backtracking: Combinations** - generating valid combinations

## Social Post Template

"Day 15/31 DSA: Backtracking = DFS + undo. It's like exploring a maze, marking paths, then erasing marks. Drawing trees helps SO much. #100DaysOfCode #Backtracking"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
