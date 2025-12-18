# Day 13: BFS Applications

## Overview

**Topic**: Applying BFS template to more complex tree problems
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 12 completed (BFS level order traversal)
- BFS template memorized
- Understanding of queue operations

## Time Breakdown

- **Review (10 min)**: Review BFS template from Day 12
- **Learn (40 min)**: Solve 2 BFS variation problems
- **Reflect (10 min)**: Optimize code for readability

## Resources

- [LeetCode 199 - Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/)
- [LeetCode 103 - Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

## Tasks

### Task 1: Review BFS Template (5 min)

Recall the core BFS pattern:

1. Initialize queue with root
2. While queue not empty:
   - Get current level size
   - Process all nodes at this level
   - Add children for next level

### Task 2: Solve LeetCode 199 - Right Side View (20 min)

- **Problem**: [LeetCode 199](https://leetcode.com/problems/binary-tree-right-side-view/)
- **Pattern**: BFS, but only keep last node of each level
- **Approach**:
  1. Standard level order traversal
  2. For each level, only add the rightmost (last) node to result
- **Time Complexity**: O(n)
- **Space Complexity**: O(w) where w is max width

```python
from collections import deque

def rightSideView(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level_size = len(queue)

        for i in range(level_size):
            node = queue.popleft()

            # Only add last node of each level
            if i == level_size - 1:
                result.append(node.val)

            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

    return result
```

**Alternative DFS approach:**

```python
def rightSideView(root):
    result = []

    def dfs(node, level):
        if not node:
            return

        # First time reaching this level
        if level == len(result):
            result.append(node.val)

        # Visit right first to see right side
        dfs(node.right, level + 1)
        dfs(node.left, level + 1)

    dfs(root, 0)
    return result
```

### Task 3: Solve LeetCode 103 - Zigzag Traversal (25 min)

- **Problem**: [LeetCode 103](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)
- **Pattern**: BFS with alternating direction
- **Approach**:
  1. Standard level order traversal
  2. Alternate: even levels left→right, odd levels right→left
- **Time Complexity**: O(n)
- **Space Complexity**: O(w)

```python
from collections import deque

def zigzagLevelOrder(root):
    if not root:
        return []

    result = []
    queue = deque([root])
    left_to_right = True

    while queue:
        level_size = len(queue)
        level_nodes = []

        for _ in range(level_size):
            node = queue.popleft()
            level_nodes.append(node.val)

            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

        # Reverse alternate levels
        if not left_to_right:
            level_nodes.reverse()

        result.append(level_nodes)
        left_to_right = not left_to_right

    return result
```

**Cleaner with deque insertion:**

```python
from collections import deque

def zigzagLevelOrder(root):
    if not root:
        return []

    result = []
    queue = deque([root])
    left_to_right = True

    while queue:
        level_size = len(queue)
        level_deque = deque()

        for _ in range(level_size):
            node = queue.popleft()

            # Add to front or back based on direction
            if left_to_right:
                level_deque.append(node.val)
            else:
                level_deque.appendleft(node.val)

            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

        result.append(list(level_deque))
        left_to_right = not left_to_right

    return result
```

### Task 4: Optimize for Readability (10 min)

Review both solutions and:

- Add meaningful variable names
- Extract common patterns
- Add comments for complex logic

**Code Review Checklist:**

- [ ] Variable names are descriptive
- [ ] No magic numbers
- [ ] Logic is easy to follow
- [ ] Edge cases handled at start

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 199, LC 103)
- [ ] Code review notes: "Made my BFS cleaner by..."
- [ ] Both BFS and DFS approaches for right side view

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain the zigzag alternation logic
- Code is clean and readable

## Success Criteria

- [ ] Can adapt BFS template to new requirements
- [ ] Understand multiple approaches to same problem
- [ ] Code is optimized for readability
- [ ] Template works for various BFS problems

## Common Pitfalls

- **Off-by-one for right side**: Use `i == level_size - 1`, not `i == level_size`
- **Wrong direction tracking**: Initialize and flip correctly
- **Reversing vs building in order**: Both work, choose cleaner approach
- **Forgetting empty tree check**: Always check `if not root`

## Next Steps

Tomorrow you'll work on: **Day 14 - Week 2 Review** - Trees & recursion consolidation with LCA

## Social Post Template

"Day 13/31 DSA: Applied BFS template to 2 new problems. Template worked perfectly. Pattern recognition >>> memorizing solutions. #100DaysOfCode #CodePatterns"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
