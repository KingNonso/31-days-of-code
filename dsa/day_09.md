# Day 9: Binary Trees - Traversals

## Overview

**Topic**: Tree data structure and DFS traversal orders
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 8 completed (recursion basics)
- Understanding of recursive function calls
- Familiarity with tree terminology (root, node, left/right child)

## Time Breakdown

- **Review (10 min)**: Review recursion checklist from Day 8
- **Learn (40 min)**: Video + implement 3 traversal types
- **Reflect (10 min)**: Memorize traversal mnemonics

## Resources

- [NeetCode Tree Traversals](https://www.youtube.com/watch?v=WLvU5EQVZqY) (15 min)
- [LeetCode 144 - Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)
- [LeetCode 94 - Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

## Tasks

### Task 1: Watch Tree Traversals Video (15 min)

Understand the three DFS traversal orders:

- **Preorder**: Root → Left → Right (NLR)
- **Inorder**: Left → Root → Right (LNR)
- **Postorder**: Left → Right → Root (LRN)

### Task 2: Solve LeetCode 144 - Preorder Traversal (12 min)

- **Problem**: [LeetCode 144](https://leetcode.com/problems/binary-tree-preorder-traversal/)
- **Pattern**: Visit root first, then recurse left, then right
- **Time Complexity**: O(n) - visit each node once
- **Space Complexity**: O(h) - height of tree (call stack)

```python
def preorderTraversal(root):
    result = []

    def dfs(node):
        if not node:
            return
        result.append(node.val)  # Process root first
        dfs(node.left)           # Then left subtree
        dfs(node.right)          # Then right subtree

    dfs(root)
    return result
```

### Task 3: Solve LeetCode 94 - Inorder Traversal (13 min)

- **Problem**: [LeetCode 94](https://leetcode.com/problems/binary-tree-inorder-traversal/)
- **Pattern**: Recurse left first, then visit root, then recurse right
- **Key Insight**: For BST, inorder gives sorted order!

```python
def inorderTraversal(root):
    result = []

    def dfs(node):
        if not node:
            return
        dfs(node.left)           # First left subtree
        result.append(node.val)  # Then process root
        dfs(node.right)          # Then right subtree

    dfs(root)
    return result
```

### Task 4: Implement Postorder Traversal (10 min)

Not a LeetCode problem, but implement it:

```python
def postorderTraversal(root):
    result = []

    def dfs(node):
        if not node:
            return
        dfs(node.left)           # First left subtree
        dfs(node.right)          # Then right subtree
        result.append(node.val)  # Process root last

    dfs(root)
    return result
```

**Use cases:**

- Preorder: Copy tree, serialize tree
- Inorder: BST gives sorted order
- Postorder: Delete tree, evaluate expression tree

### Task 5: Create Traversal Mnemonic Sheet (10 min)

| Traversal | Order           | Mnemonic            | Use Case            |
| --------- | --------------- | ------------------- | ------------------- |
| Preorder  | Root→Left→Right | "**P**arent first"  | Copy/serialize tree |
| Inorder   | Left→Root→Right | "**I**n the middle" | BST sorted order    |
| Postorder | Left→Right→Root | "**P**arent last"   | Delete tree         |

**Visual Example:**

```
    1
   / \
  2   3
 / \
4   5

Preorder:  1, 2, 4, 5, 3
Inorder:   4, 2, 5, 1, 3
Postorder: 4, 5, 2, 3, 1
```

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 144, LC 94)
- [ ] Postorder implementation (tested locally)
- [ ] Mnemonic sheet: traversal orders with mnemonics and use cases

## Validation

How to verify you completed the work:

- Both LeetCode solutions accepted
- Can recite all three traversal orders from memory
- Can trace through a tree and write output for each traversal

## Success Criteria

- [ ] Understand DFS tree traversal concept
- [ ] Can implement all 3 traversals recursively
- [ ] Know when to use each traversal type
- [ ] Memorized mnemonics for traversal orders

## Common Pitfalls

- **Forgetting base case**: Always check if node is None
- **Wrong order of operations**: Remember where `result.append()` goes
- **Confusing traversal names**: Use mnemonics to remember
- **Not understanding call stack**: Draw the recursion tree

## Next Steps

Tomorrow you'll work on: **Day 10 - Binary Trees: DFS Problems** - max depth, diameter

## Social Post Template

"Day 9/31 DSA: Tree traversals unlocked. Preorder = root→left→right. Inorder = left→root→right. Recursion makes it elegant. #100DaysOfCode #BinaryTrees"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
