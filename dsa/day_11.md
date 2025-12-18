# Day 11: Binary Search Trees

## Overview

**Topic**: BST properties, search, and validation
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Days 9-10 completed (tree traversals, DFS problems)
- Understanding of binary tree structure
- Familiarity with comparison operators

## Time Breakdown

- **Review (10 min)**: Review tree DFS patterns
- **Learn (40 min)**: Understand BST property + solve 2 problems
- **Reflect (10 min)**: Document BST property and common mistakes

## Resources

- [LeetCode 700 - Search in a BST](https://leetcode.com/problems/search-in-a-binary-search-tree/)
- [LeetCode 98 - Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

## BST Property

**Binary Search Tree Rule**: For every node:

- All values in **left subtree** are **less than** node's value
- All values in **right subtree** are **greater than** node's value
- This applies to ALL descendants, not just immediate children

```
        8
       / \
      3   10
     / \    \
    1   6   14
       / \
      4   7
```

This is a valid BST because every node satisfies the property.

## Tasks

### Task 1: Understand BST Property (10 min)

Key insight: BST property is **global**, not just local.

**Invalid BST (common mistake):**

```
    5
   / \
  3   7
 / \
1   6  ← 6 > 5 (root), so invalid!
```

Even though 6 > 3 (its parent), it's still in the left subtree of 5, so it must be < 5.

### Task 2: Solve LeetCode 700 - Search in BST (15 min)

- **Problem**: [LeetCode 700](https://leetcode.com/problems/search-in-a-binary-search-tree/)
- **Pattern**: Binary search on tree structure
- **Approach**:
  1. If current node is target, return it
  2. If target < current, search left
  3. If target > current, search right
- **Time Complexity**: O(h) where h is height (O(log n) balanced, O(n) skewed)
- **Space Complexity**: O(h) recursive, O(1) iterative

```python
def searchBST(root, val):
    if not root:
        return None

    if val == root.val:
        return root
    elif val < root.val:
        return searchBST(root.left, val)
    else:
        return searchBST(root.right, val)
```

**Iterative Version:**

```python
def searchBST(root, val):
    while root and root.val != val:
        root = root.left if val < root.val else root.right
    return root
```

### Task 3: Solve LeetCode 98 - Validate BST (25 min)

- **Problem**: [LeetCode 98](https://leetcode.com/problems/validate-binary-search-tree/)
- **Pattern**: DFS with valid range tracking
- **Key Insight**: Each node must be within a valid range
- **Approach**: Track (min, max) bounds as you traverse

```python
def isValidBST(root):
    def validate(node, min_val, max_val):
        if not node:
            return True

        # Check current node against bounds
        if node.val <= min_val or node.val >= max_val:
            return False

        # Left subtree: update max bound to current value
        # Right subtree: update min bound to current value
        return (validate(node.left, min_val, node.val) and
                validate(node.right, node.val, max_val))

    return validate(root, float('-inf'), float('inf'))
```

**Why this works:**

- Going left: node must be less than parent → update max
- Going right: node must be greater than parent → update min

**Alternative: Inorder traversal should be strictly increasing**

```python
def isValidBST(root):
    prev = float('-inf')

    def inorder(node):
        nonlocal prev
        if not node:
            return True

        if not inorder(node.left):
            return False

        if node.val <= prev:
            return False
        prev = node.val

        return inorder(node.right)

    return inorder(root)
```

### Task 4: Document BST Property (10 min)

Create documentation:

**BST Key Points:**

1. Property is GLOBAL (all descendants, not just children)
2. Inorder traversal gives sorted order
3. Search is O(log n) for balanced, O(n) for skewed
4. Validation requires tracking valid range

**Common BST Mistakes:**

- Only checking immediate children
- Forgetting equal values (typically not allowed in BST)
- Not handling negative infinity / positive infinity bounds

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 700, LC 98)
- [ ] Documentation: BST property with examples
- [ ] Explanation of why local checking fails for validation

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can explain why the "6 under 3" example is invalid
- Understand both validation approaches (bounds vs inorder)

## Success Criteria

- [ ] Understand BST property at deep level (global, not local)
- [ ] Can search BST in O(log n)
- [ ] Can validate BST using range tracking
- [ ] Know alternative inorder validation approach

## Common Pitfalls

- **Local checking only**: Must consider all ancestors
- **Inclusive vs exclusive bounds**: BSTs typically require strictly less/greater
- **Integer overflow**: Use float('-inf') and float('inf') for bounds
- **Forgetting base case**: Empty tree is valid BST

## Next Steps

Tomorrow you'll work on: **Day 12 - BFS: Level Order Traversal** - queue-based breadth-first search

## Social Post Template

"Day 11/31 DSA: BST validation taught me: local checks aren't enough. Need to track valid range for each node. Devil in the details. #100DaysOfCode #BST"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
