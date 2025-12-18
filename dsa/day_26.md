# Day 26: Graph - Shortest Path (Dijkstra)

## Overview

**Topic**: Weighted shortest path with Dijkstra's algorithm
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 25 completed (graph BFS/DFS)
- Day 18 completed (heaps)
- Understanding of weighted graphs

## Time Breakdown

- **Review (10 min)**: Review BFS for unweighted shortest path
- **Learn (40 min)**: Video + solve network delay problem
- **Reflect (10 min)**: Document Dijkstra template

## Resources

- [Dijkstra Explanation](https://www.youtube.com/watch?v=pSqmAO-m7Lk) (15 min)
- [LeetCode 743 - Network Delay Time](https://leetcode.com/problems/network-delay-time/)

## Why Dijkstra?

- **BFS**: Works for unweighted graphs (all edges = 1)
- **Dijkstra**: Works for weighted graphs with non-negative edges
- **Key idea**: Always process the closest unvisited node first

## Tasks

### Task 1: Watch Dijkstra Video (15 min)

Understand:

- Why BFS doesn't work for weighted graphs
- Priority queue (min-heap) to get closest node
- Relaxation: update distance if shorter path found

### Task 2: Understand Dijkstra Template (10 min)

```python
import heapq

def dijkstra(graph, start):
    # graph: {node: [(neighbor, weight), ...]}
    distances = {node: float('inf') for node in graph}
    distances[start] = 0

    # Min-heap: (distance, node)
    heap = [(0, start)]

    while heap:
        dist, node = heapq.heappop(heap)

        # Skip if we've found better path
        if dist > distances[node]:
            continue

        for neighbor, weight in graph[node]:
            new_dist = dist + weight
            if new_dist < distances[neighbor]:
                distances[neighbor] = new_dist
                heapq.heappush(heap, (new_dist, neighbor))

    return distances
```

**Time Complexity**: O((V + E) log V)
**Space Complexity**: O(V)

### Task 3: Solve LeetCode 743 - Network Delay Time (25 min)

- **Problem**: [LeetCode 743](https://leetcode.com/problems/network-delay-time/)
- **Pattern**: Dijkstra's algorithm
- **Goal**: Find max of shortest paths from source to all nodes

```python
import heapq
from collections import defaultdict

def networkDelayTime(times, n, k):
    # Build adjacency list
    graph = defaultdict(list)
    for u, v, w in times:
        graph[u].append((v, w))

    # Dijkstra's algorithm
    distances = {i: float('inf') for i in range(1, n + 1)}
    distances[k] = 0

    heap = [(0, k)]  # (distance, node)

    while heap:
        dist, node = heapq.heappop(heap)

        # Skip if already processed with shorter distance
        if dist > distances[node]:
            continue

        for neighbor, weight in graph[node]:
            new_dist = dist + weight
            if new_dist < distances[neighbor]:
                distances[neighbor] = new_dist
                heapq.heappush(heap, (new_dist, neighbor))

    # Find max distance (time for all nodes to receive signal)
    max_dist = max(distances.values())
    return max_dist if max_dist != float('inf') else -1
```

**Key Points:**

- Build graph from edge list
- Use min-heap to always process closest node
- Return max distance (all nodes must receive signal)
- Return -1 if any node unreachable

### Task 4: Document Shortest Path Patterns (10 min)

**Shortest Path Algorithms:**

| Algorithm      | Graph Type           | Time Complexity | Use When                |
| -------------- | -------------------- | --------------- | ----------------------- |
| BFS            | Unweighted           | O(V + E)        | All edges same weight   |
| Dijkstra       | Non-negative weights | O((V+E) log V)  | Positive weights        |
| Bellman-Ford   | Any weights          | O(V \* E)       | Negative weights        |
| Floyd-Warshall | Any                  | O(V³)           | All pairs shortest path |

**Dijkstra Key Points:**

1. Use min-heap (priority queue)
2. Process nodes in order of distance
3. "Relax" edges: update if shorter path found
4. Works only with non-negative edges

**Template: Dijkstra = BFS + Priority Queue**

```
BFS uses: Queue (FIFO)
Dijkstra uses: Priority Queue (min-heap by distance)
```

## Output Requirements

What you must produce today:

- [ ] Accepted solution for LC 743
- [ ] Dijkstra template documented
- [ ] Understanding of when to use Dijkstra vs BFS

## Validation

How to verify you completed the work:

- Solution accepted
- Can trace through Dijkstra step by step
- Understand why heap is needed

## Success Criteria

- [ ] Understand Dijkstra's algorithm
- [ ] Know when BFS vs Dijkstra
- [ ] Can implement Dijkstra with heap
- [ ] Network delay problem solved

## Common Pitfalls

- **Using BFS for weighted graphs**: Gives wrong answer
- **Not checking if already processed**: Causes inefficiency
- **Negative weights**: Dijkstra doesn't work (use Bellman-Ford)
- **Forgetting unreachable nodes**: Check for infinity

## Next Steps

Tomorrow you'll work on: **Day 27 - Graph: Topological Sort** - cycle detection, course schedule

## Social Post Template

"Day 26/31 DSA: Dijkstra = greedy BFS with heap. Always process nearest unvisited node. Network Delay was challenging but template works! #100DaysOfCode #ShortestPath"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
