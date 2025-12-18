# Day 14: Week 2 Review - Trees & Recursion

## Overview

**Topic**: Consolidate Week 2 with LCA problem + create decision flowchart
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate (Checkpoint)

## Prerequisites

- Days 8-13 completed
- All tree patterns practiced
- Understanding of DFS and BFS

## Time Breakdown

- **Review (15 min)**: Review all tree patterns from Week 2
- **Learn (35 min)**: Solve Lowest Common Ancestor
- **Reflect (10 min)**: Create decision flowchart for tree problems

## Resources

- [LeetCode 236 - Lowest Common Ancestor of Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
- Your pattern docs from Days 8-13

## Patterns to Review

### Day 8: Recursion Basics

- Base case → Recursive case → Return value
- Trust the recursion, don't trace every call

### Day 9: Tree Traversals (DFS)

- Preorder: Root → Left → Right
- Inorder: Left → Root → Right
- Postorder: Left → Right → Root

### Day 10: DFS Tree Problems

- Bottom-up: compute from children
- Top-down: pass info to children
- Hybrid: use global variable

### Day 11: Binary Search Trees

- Property: all left < root < all right (global)
- Inorder gives sorted order

### Days 12-13: BFS

- Queue-based level order
- Use for level problems, shortest path

## Tasks

### Task 1: Review All Tree Patterns (15 min)

Go through each pattern:

- Recall the template code
- Remember key problems
- Note which patterns feel weak

### Task 2: Solve LeetCode 236 - Lowest Common Ancestor (35 min)

- **Problem**: [LeetCode 236](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)
- **Pattern**: Bottom-up DFS with path tracking
- **Difficulty**: This is tricky - take your time!

**Approach 1: Recursive (Elegant)**

```python
def lowestCommonAncestor(root, p, q):
    # Base cases
    if not root:
        return None
    if root == p or root == q:
        return root

    # Search in left and right subtrees
    left = lowestCommonAncestor(root.left, p, q)
    right = lowestCommonAncestor(root.right, p, q)

    # If both found something, current node is LCA
    if left and right:
        return root

    # Otherwise, return whichever found something
    return left if left else right
```

**Why this works:**

1. If current node is p or q, return it
2. Recurse on both subtrees
3. If both subtrees return non-null, current node is LCA
4. If only one returns non-null, that's where both nodes are

**Approach 2: Parent Pointers (Alternative)**

```python
def lowestCommonAncestor(root, p, q):
    # Build parent map
    parent = {root: None}
    stack = [root]

    while p not in parent or q not in parent:
        node = stack.pop()
        if node.left:
            parent[node.left] = node
            stack.append(node.left)
        if node.right:
            parent[node.right] = node
            stack.append(node.right)

    # Build ancestors set for p
    ancestors = set()
    while p:
        ancestors.add(p)
        p = parent[p]

    # Find first ancestor of q that's also ancestor of p
    while q not in ancestors:
        q = parent[q]

    return q
```

### Task 3: Create Decision Flowchart (10 min)

**Tree Problem Decision Tree:**

```
Is it a tree problem?
│
├── Need level-by-level processing?
│   └── YES → Use BFS (queue)
│
├── Need to find path or explore all possibilities?
│   └── YES → Use DFS (recursion/stack)
│
├── Is it a BST?
│   ├── YES → Can you use BST property to eliminate half the tree?
│   │   └── YES → Binary search approach (O(log n))
│   └── NO → Regular tree traversal
│
├── Need info from children to compute parent?
│   └── YES → Bottom-up DFS (postorder-like)
│
├── Need to pass info from parent to children?
│   └── YES → Top-down DFS (preorder-like)
│
└── Need both parent→child AND child→parent info?
    └── YES → Hybrid with global variable
```

## Output Requirements

What you must produce today:

- [ ] LCA solution accepted on LeetCode
- [ ] Decision flowchart for tree problems
- [ ] Can explain both LCA approaches

## Validation

How to verify you completed the work:

- LCA solution passes all test cases
- Flowchart covers all Week 2 patterns
- Can choose BFS vs DFS appropriately

## Checkpoint Questions

Answer these to validate Week 2 learning:

1. What's the difference between preorder and postorder? (When root is processed)
2. When should you use BFS over DFS? (Level processing, shortest path)
3. Why does BST inorder give sorted order? (Left < Root < Right, always)
4. How do you validate a BST? (Track valid range for each node)
5. What's the time complexity of tree traversal? (O(n))

## Success Criteria

- [ ] Solved LCA problem independently
- [ ] Can write recursive tree solutions without templates
- [ ] Can choose BFS vs DFS appropriately
- [ ] Understand bottom-up vs top-down DFS

## Common Pitfalls

- **LCA: Missing base cases**: Must handle root == p or q
- **LCA: Wrong return logic**: Return root when both children find something
- **Confusing BFS/DFS use cases**: BFS for levels, DFS for paths
- **Not trusting recursion**: Try to trace every call mentally

## Next Steps

Tomorrow you'll work on: **Day 15 - Backtracking Fundamentals** - explore all possibilities with pruning

## Social Post Template

"Week 2/31 DSA done! Trees demystified: DFS for path problems, BFS for levels. Recursion is now my friend. LCA problem was tough but satisfying. 💪 #100DaysOfCode #BinaryTrees"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
