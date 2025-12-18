# Day 10: Binary Trees - DFS Problems

## Overview

**Topic**: Depth-first search for tree properties (depth, diameter, paths)
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 9 completed (tree traversals)
- Understanding of recursion and return values
- Familiarity with tree height concept

## Time Breakdown

- **Review (10 min)**: Review traversal patterns from Day 9
- **Learn (40 min)**: Solve 2 DFS tree problems
- **Reflect (10 min)**: Document DFS tree pattern

## Resources

- [LeetCode 104 - Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [LeetCode 543 - Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

## Tasks

### Task 1: Review Day 9 Traversals (5 min)

Recall:

- Tree traversal is just visiting nodes in specific order
- DFS uses recursion (or stack) to go deep first
- Each node is visited exactly once → O(n)

### Task 2: Solve LeetCode 104 - Max Depth (15 min)

- **Problem**: [LeetCode 104](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- **Pattern**: Bottom-up DFS - compute height from leaves
- **Approach**:
  1. Base case: empty node has depth 0
  2. Recursive case: max(left_depth, right_depth) + 1
- **Time Complexity**: O(n)
- **Space Complexity**: O(h) - tree height

```python
def maxDepth(root):
    if not root:
        return 0

    left_depth = maxDepth(root.left)
    right_depth = maxDepth(root.right)

    return max(left_depth, right_depth) + 1
```

**Key Insight**: Trust the recursion - assume `maxDepth(root.left)` correctly returns left subtree's depth.

### Task 3: Solve LeetCode 543 - Diameter (25 min)

- **Problem**: [LeetCode 543](https://leetcode.com/problems/diameter-of-binary-tree/)
- **Pattern**: DFS with global variable (or nonlocal)
- **Key Insight**: Diameter at each node = left_height + right_height
- **Approach**:
  1. At each node, calculate diameter through this node
  2. Track maximum diameter seen globally
  3. Return height for parent's calculation

```python
def diameterOfBinaryTree(root):
    diameter = 0

    def height(node):
        nonlocal diameter
        if not node:
            return 0

        left_height = height(node.left)
        right_height = height(node.right)

        # Diameter through this node
        diameter = max(diameter, left_height + right_height)

        # Return height for parent
        return max(left_height, right_height) + 1

    height(root)
    return diameter
```

**Why global variable?** The function returns height (for recursion), but we need to track diameter (the answer). These are different values!

### Task 4: Document DFS Tree Pattern (10 min)

Create pattern documentation:

**DFS Tree Problem Types:**

1. **Bottom-up** (like max depth):

   - Compute result from children, return to parent
   - Return value is the answer

2. **Top-down** (like path sum):

   - Pass information from parent to children
   - Parameters carry state

3. **Hybrid** (like diameter):
   - Need both child info AND track global state
   - Use helper function with global/nonlocal variable

**Template for Hybrid Problems:**

```python
def solve(root):
    result = initial_value  # Global tracker

    def dfs(node):
        nonlocal result
        if not node:
            return base_case

        left = dfs(node.left)
        right = dfs(node.right)

        # Update global result
        result = update(result, left, right)

        # Return value for parent
        return compute(left, right)

    dfs(root)
    return result
```

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 104, LC 543)
- [ ] DFS pattern doc: when to use helper functions + global state
- [ ] Explanation of why diameter needs different return value than answer

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain the "global variable trick" for diameter
- Understand difference between bottom-up and top-down DFS

## Success Criteria

- [ ] Can implement bottom-up DFS for tree properties
- [ ] Understand when to use global/nonlocal variables
- [ ] Can trace through diameter calculation step by step
- [ ] Both problems solved optimally

## Common Pitfalls

- **Confusing height vs depth**: Height is from node to leaf, depth is from root to node
- **Forgetting to update global variable**: Make sure `diameter = max(...)` executes
- **Wrong return value**: Return height, not diameter, from helper
- **Not handling empty tree**: Check `if not root` at start

## Next Steps

Tomorrow you'll work on: **Day 11 - Binary Search Trees** - BST properties and validation

## Social Post Template

"Day 10/31 DSA: Binary tree DFS pattern emerging. Key insight: diameter needs info from both subtrees. Helper functions are your friend. #100DaysOfCode #TreeProblems"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
