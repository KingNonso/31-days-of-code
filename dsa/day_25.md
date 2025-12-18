# Day 25: Graph - BFS/DFS Basics

## Overview

**Topic**: Graph traversal with DFS and BFS on grids and adjacency lists
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Week 2 completed (tree BFS/DFS)
- Understanding of recursion
- Familiarity with 2D arrays

## Time Breakdown

- **Review (10 min)**: Review tree BFS/DFS
- **Learn (40 min)**: Solve 2 graph problems
- **Reflect (10 min)**: Document graph representations

## Resources

- [LeetCode 200 - Number of Islands](https://leetcode.com/problems/number-of-islands/)
- [LeetCode 133 - Clone Graph](https://leetcode.com/problems/clone-graph/)

## Graph Representations

**Adjacency List** (most common):

```python
graph = {
    0: [1, 2],
    1: [0, 3],
    2: [0, 3],
    3: [1, 2]
}
```

**Adjacency Matrix**:

```python
# matrix[i][j] = 1 if edge between i and j
matrix = [
    [0, 1, 1, 0],
    [1, 0, 0, 1],
    [1, 0, 0, 1],
    [0, 1, 1, 0]
]
```

**Grid as Graph**: Each cell is a node, adjacent cells are neighbors

## Tasks

### Task 1: Understand Graph vs Tree (5 min)

Key differences:

- **Tree**: No cycles, single path between nodes
- **Graph**: May have cycles, need to track visited nodes
- **Both**: Use BFS/DFS for traversal

### Task 2: Solve LeetCode 200 - Number of Islands (25 min)

- **Problem**: [LeetCode 200](https://leetcode.com/problems/number-of-islands/)
- **Pattern**: DFS/BFS on grid, count connected components
- **Approach**: For each unvisited land cell, DFS to mark entire island

**DFS Solution:**

```python
def numIslands(grid):
    if not grid:
        return 0

    rows, cols = len(grid), len(grid[0])
    count = 0

    def dfs(r, c):
        # Out of bounds or water or visited
        if (r < 0 or r >= rows or
            c < 0 or c >= cols or
            grid[r][c] != '1'):
            return

        # Mark as visited
        grid[r][c] = '#'

        # Visit all 4 neighbors
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                count += 1
                dfs(r, c)

    return count
```

**BFS Solution:**

```python
from collections import deque

def numIslands(grid):
    if not grid:
        return 0

    rows, cols = len(grid), len(grid[0])
    count = 0

    def bfs(r, c):
        queue = deque([(r, c)])
        grid[r][c] = '#'

        while queue:
            row, col = queue.popleft()
            for dr, dc in [(1,0), (-1,0), (0,1), (0,-1)]:
                nr, nc = row + dr, col + dc
                if (0 <= nr < rows and
                    0 <= nc < cols and
                    grid[nr][nc] == '1'):
                    grid[nr][nc] = '#'
                    queue.append((nr, nc))

    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                count += 1
                bfs(r, c)

    return count
```

**Time Complexity**: O(m _ n)
**Space Complexity**: O(m _ n) worst case for stack/queue

### Task 3: Solve LeetCode 133 - Clone Graph (20 min)

- **Problem**: [LeetCode 133](https://leetcode.com/problems/clone-graph/)
- **Pattern**: BFS/DFS with hash map to track cloned nodes
- **Key**: Map original node → cloned node to handle cycles

```python
def cloneGraph(node):
    if not node:
        return None

    # Map from original node to cloned node
    cloned = {}

    def dfs(n):
        if n in cloned:
            return cloned[n]

        # Create clone
        clone = Node(n.val)
        cloned[n] = clone

        # Clone neighbors
        for neighbor in n.neighbors:
            clone.neighbors.append(dfs(neighbor))

        return clone

    return dfs(node)
```

**BFS Version:**

```python
from collections import deque

def cloneGraph(node):
    if not node:
        return None

    cloned = {node: Node(node.val)}
    queue = deque([node])

    while queue:
        n = queue.popleft()
        for neighbor in n.neighbors:
            if neighbor not in cloned:
                cloned[neighbor] = Node(neighbor.val)
                queue.append(neighbor)
            cloned[n].neighbors.append(cloned[neighbor])

    return cloned[node]
```

### Task 4: Document Graph Patterns (10 min)

**Graph Representation Comparison:**

| Representation   | Space  | Edge Check | Iterate Neighbors |
| ---------------- | ------ | ---------- | ----------------- |
| Adjacency List   | O(V+E) | O(degree)  | O(degree)         |
| Adjacency Matrix | O(V²)  | O(1)       | O(V)              |
| Edge List        | O(E)   | O(E)       | O(E)              |

**When to Use Each:**

- **Adjacency List**: Sparse graphs (most problems)
- **Adjacency Matrix**: Dense graphs, need O(1) edge check
- **Grid**: Implicit graph (cells are nodes)

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 200, LC 133)
- [ ] DFS and BFS solutions for at least one problem
- [ ] Graph representation comparison table

## Validation

How to verify you completed the work:

- Both solutions accepted
- Can implement both DFS and BFS for graphs
- Understand visited tracking importance

## Success Criteria

- [ ] Understand graph traversal patterns
- [ ] Can handle grid as implicit graph
- [ ] Know when to use hash map for visited tracking
- [ ] Both problems solved

## Common Pitfalls

- **Not tracking visited**: Causes infinite loops in graphs with cycles
- **Wrong neighbor iteration**: Grid uses 4 directions, graph uses neighbor list
- **Modifying input**: Sometimes okay (islands), sometimes not (clone)
- **Off-by-one in grid bounds**: Always check bounds first

## Next Steps

Tomorrow you'll work on: **Day 26 - Graph: Shortest Path** - Dijkstra's algorithm

## Social Post Template

"Day 25/31 DSA: Graphs = nodes + edges. Islands = connected components. DFS/BFS on grids = mark visited. Adjacency list > matrix usually. #100DaysOfCode #GraphTheory"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
