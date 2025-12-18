# Day 27: Graph - Cycle Detection & Topological Sort

## Overview

**Topic**: Detecting cycles and ordering dependencies with topological sort
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Days 25-26 completed (graph traversal, Dijkstra)
- Understanding of DFS
- Familiarity with directed graphs

## Time Breakdown

- **Review (10 min)**: Review graph DFS
- **Learn (40 min)**: Solve Course Schedule I and II
- **Reflect (10 min)**: Document topological sort patterns

## Resources

- [LeetCode 207 - Course Schedule](https://leetcode.com/problems/course-schedule/)
- [LeetCode 210 - Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)

## What is Topological Sort?

- Linear ordering of vertices in a DAG (Directed Acyclic Graph)
- If edge u→v exists, u comes before v in ordering
- Used for: task scheduling, build systems, dependency resolution

**Note**: Topological sort only exists for DAGs (no cycles!)

## Tasks

### Task 1: Understand Cycle Detection (10 min)

**DFS-based cycle detection:**

- Track node states: unvisited, visiting, visited
- Cycle exists if we reach a "visiting" node

**States:**

- `0` = unvisited
- `1` = visiting (in current DFS path)
- `2` = visited (completely processed)

### Task 2: Solve LeetCode 207 - Course Schedule (20 min)

- **Problem**: [LeetCode 207](https://leetcode.com/problems/course-schedule/)
- **Pattern**: Cycle detection in directed graph
- **Key Insight**: If cycle exists, can't complete all courses

```python
def canFinish(numCourses, prerequisites):
    # Build adjacency list
    graph = [[] for _ in range(numCourses)]
    for course, prereq in prerequisites:
        graph[prereq].append(course)

    # 0 = unvisited, 1 = visiting, 2 = visited
    state = [0] * numCourses

    def hasCycle(node):
        if state[node] == 1:  # Found cycle
            return True
        if state[node] == 2:  # Already processed
            return False

        state[node] = 1  # Mark as visiting

        for neighbor in graph[node]:
            if hasCycle(neighbor):
                return True

        state[node] = 2  # Mark as visited
        return False

    for course in range(numCourses):
        if hasCycle(course):
            return False

    return True
```

**Time Complexity**: O(V + E)
**Space Complexity**: O(V)

### Task 3: Solve LeetCode 210 - Course Schedule II (20 min)

- **Problem**: [LeetCode 210](https://leetcode.com/problems/course-schedule-ii/)
- **Pattern**: Topological sort
- **Key Insight**: DFS postorder gives reverse topological order

```python
def findOrder(numCourses, prerequisites):
    # Build adjacency list
    graph = [[] for _ in range(numCourses)]
    for course, prereq in prerequisites:
        graph[prereq].append(course)

    state = [0] * numCourses
    result = []

    def dfs(node):
        if state[node] == 1:  # Cycle
            return False
        if state[node] == 2:  # Already processed
            return True

        state[node] = 1

        for neighbor in graph[node]:
            if not dfs(neighbor):
                return False

        state[node] = 2
        result.append(node)  # Add after processing all descendants
        return True

    for course in range(numCourses):
        if not dfs(course):
            return []  # Cycle exists

    return result[::-1]  # Reverse for correct order
```

**Alternative: Kahn's Algorithm (BFS)**

```python
from collections import deque

def findOrder(numCourses, prerequisites):
    graph = [[] for _ in range(numCourses)]
    in_degree = [0] * numCourses

    for course, prereq in prerequisites:
        graph[prereq].append(course)
        in_degree[course] += 1

    # Start with nodes having no prerequisites
    queue = deque([i for i in range(numCourses) if in_degree[i] == 0])
    result = []

    while queue:
        node = queue.popleft()
        result.append(node)

        for neighbor in graph[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)

    return result if len(result) == numCourses else []
```

### Task 4: Document Topological Sort Patterns (10 min)

**Two Approaches:**

| Approach     | How it works                                 | Output          |
| ------------ | -------------------------------------------- | --------------- |
| DFS          | Process descendants first, reverse postorder | Reversed result |
| BFS (Kahn's) | Process nodes with 0 in-degree first         | Direct result   |

**When to Use:**

- **Cycle detection only**: DFS with 3 states
- **Need ordering**: Either DFS (reverse) or BFS (direct)
- **Prefer BFS**: When you want ordering in natural order

**Key Insight:**

- DFS topological sort adds node AFTER all descendants processed
- BFS topological sort processes nodes WHEN all prerequisites done

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions (LC 207, LC 210)
- [ ] Both DFS and BFS approaches for Course Schedule II
- [ ] Documentation of cycle detection + topological sort

## Validation

How to verify you completed the work:

- Both solutions accepted
- Understand 3-state DFS for cycle detection
- Can implement both DFS and BFS topological sort

## Success Criteria

- [ ] Understand cycle detection with 3 states
- [ ] Can implement topological sort
- [ ] Know DFS vs BFS approaches
- [ ] Both problems solved

## Common Pitfalls

- **2-state vs 3-state**: Need 3 states for directed graph cycles
- **Wrong graph direction**: prereq → course, not course → prereq
- **Forgetting to reverse DFS result**: DFS gives reverse order
- **Not handling disconnected components**: Must check all nodes

## Next Steps

Tomorrow you'll work on: **Day 28 - Week 4 Review** - DP + Graph integration

## Social Post Template

"Day 27/31 DSA: Cycle detection = DFS with recursion stack tracking. Topological sort = dependencies first. Course Schedule problems make it practical! #100DaysOfCode #Graphs"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
