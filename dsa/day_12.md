# Day 12: BFS - Level Order Traversal

## Overview

**Topic**: Breadth-first search using queue for level-by-level processing
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Days 9-11 completed (tree traversals, DFS, BST)
- Understanding of queue data structure (FIFO)
- Familiarity with DFS patterns

## Time Breakdown

- **Review (10 min)**: Compare DFS stack vs BFS queue mentally
- **Learn (40 min)**: Video + solve level order problem + write template
- **Reflect (10 min)**: Create BFS vs DFS decision guide

## Resources

- [NeetCode BFS Explanation](https://www.youtube.com/watch?v=6ZnyEApgFYg) (12 min)
- [LeetCode 102 - Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

## BFS vs DFS Comparison

| Aspect         | DFS                           | BFS                           |
| -------------- | ----------------------------- | ----------------------------- |
| Data Structure | Stack (or recursion)          | Queue                         |
| Order          | Deep first, then backtrack    | Level by level                |
| Use Cases      | Path finding, tree properties | Shortest path, level problems |
| Space          | O(h) height                   | O(w) max width                |

## Tasks

### Task 1: Watch BFS Video (12 min)

Understand:

- Why queue enables level-by-level processing
- How to track which level you're on
- BFS guarantees shortest path in unweighted graphs

### Task 2: Solve LeetCode 102 - Level Order Traversal (25 min)

- **Problem**: [LeetCode 102](https://leetcode.com/problems/binary-tree-level-order-traversal/)
- **Pattern**: BFS with level tracking
- **Approach**:
  1. Use queue, start with root
  2. Process all nodes at current level
  3. Add their children for next level
  4. Repeat until queue empty

```python
from collections import deque

def levelOrder(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level_size = len(queue)  # Nodes at current level
        level_nodes = []

        for _ in range(level_size):
            node = queue.popleft()
            level_nodes.append(node.val)

            # Add children for next level
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

        result.append(level_nodes)

    return result
```

**Key Insight**: `level_size = len(queue)` captures how many nodes are at current level BEFORE adding children.

### Task 3: Write BFS Template (13 min)

Create reusable BFS template:

```python
from collections import deque

def bfs_tree_template(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level_size = len(queue)

        # Process current level
        for _ in range(level_size):
            node = queue.popleft()

            # Do something with node
            process(node)

            # Add children
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

        # After processing level
        after_level_processing()

    return result
```

**BFS for Graphs (with visited tracking):**

```python
def bfs_graph(start, graph):
    visited = set([start])
    queue = deque([start])

    while queue:
        node = queue.popleft()
        process(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
```

### Task 4: Create BFS vs DFS Decision Guide (10 min)

**Use BFS when:**

- Need level-by-level processing
- Finding shortest path (unweighted)
- Need to find closest/nearest
- Problem mentions "minimum steps/moves"

**Use DFS when:**

- Need to explore all paths
- Finding any path (not necessarily shortest)
- Tree/graph properties (depth, diameter)
- Backtracking problems

**Memory Trade-off:**

- BFS: O(w) where w = max width (can be O(n) for balanced tree)
- DFS: O(h) where h = height (O(log n) balanced, O(n) skewed)

## Output Requirements

What you must produce today:

- [ ] Accepted solution for LeetCode 102
- [ ] BFS template code (tree and graph versions)
- [ ] BFS vs DFS decision guide

## Validation

How to verify you completed the work:

- Solution accepted on LeetCode
- Can explain why BFS processes level by level
- Can identify when to use BFS vs DFS

## Success Criteria

- [ ] Understand queue-based BFS mechanics
- [ ] Can implement level order traversal
- [ ] Know when BFS is better than DFS
- [ ] Template ready for future BFS problems

## Common Pitfalls

- **Forgetting to track level size**: Must capture `len(queue)` before processing
- **Using list instead of deque**: `list.pop(0)` is O(n), `deque.popleft()` is O(1)
- **Not handling empty root**: Check `if not root` first
- **Confusing BFS with DFS**: BFS uses queue, DFS uses stack/recursion

## Next Steps

Tomorrow you'll work on: **Day 13 - BFS Applications** - right side view, zigzag traversal

## Social Post Template

"Day 12/31 DSA: BFS = process level by level using queue. Perfect for shortest path, level-based problems. DFS vs BFS now crystal clear. #100DaysOfCode #Algorithms"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
