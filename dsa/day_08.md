# Day 8: Recursion Basics

## Overview

**Topic**: Recursive thinking, base cases, and recursion trees
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Week 1 completed (all 6 patterns)
- Understanding of function calls and call stack
- Familiarity with mathematical induction (helpful but not required)

## Time Breakdown

- **Review (10 min)**: Review Week 1 cheat sheet
- **Learn (40 min)**: Video + 2 recursion problems + draw recursion trees
- **Reflect (10 min)**: Create recursion checklist

## Resources

- [Abdul Bari - Recursion](https://www.youtube.com/watch?v=kepBmgvWNDw) (20 min)
- [LeetCode 509 - Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)
- [LeetCode 231 - Power of Two](https://leetcode.com/problems/power-of-two/)

## Tasks

### Task 1: Watch Recursion Video (20 min)

Focus on understanding:

- What is a base case and why is it essential?
- How does the call stack work?
- How to trace through recursive calls?

### Task 2: Solve LeetCode 509 - Fibonacci (10 min)

- **Problem**: [LeetCode 509](https://leetcode.com/problems/fibonacci-number/)
- **Pattern**: Classic recursion with overlapping subproblems
- **Approach**:
  1. Base cases: F(0) = 0, F(1) = 1
  2. Recursive case: F(n) = F(n-1) + F(n-2)
- **Time Complexity**: O(2^n) - exponential (will optimize later with DP)
- **Space Complexity**: O(n) - call stack depth

```python
def fib(n):
    # Base cases
    if n <= 1:
        return n
    # Recursive case
    return fib(n - 1) + fib(n - 2)
```

### Task 3: Draw Recursion Tree for Fibonacci(5) (10 min)

Visualize the calls:

```
                    fib(5)
                   /      \
              fib(4)      fib(3)
             /    \       /    \
         fib(3)  fib(2) fib(2) fib(1)
         /   \    /  \   /  \
     fib(2) fib(1) ...  ...
```

Notice:

- Same subproblems computed multiple times (inefficient!)
- This is why we'll learn Dynamic Programming later

### Task 4: Solve LeetCode 231 - Power of Two (10 min)

- **Problem**: [LeetCode 231](https://leetcode.com/problems/power-of-two/)
- **Pattern**: Recursion with single recursive call
- **Approach**:
  1. Base cases: n <= 0 returns false, n == 1 returns true
  2. Recursive case: If n is even, check if n/2 is power of two
- **Time Complexity**: O(log n)
- **Space Complexity**: O(log n)

```python
def isPowerOfTwo(n):
    if n <= 0:
        return False
    if n == 1:
        return True
    if n % 2 != 0:
        return False
    return isPowerOfTwo(n // 2)
```

### Task 5: Create Recursion Checklist (10 min)

Every recursive function needs:

1. **Base Case(s)**: When to stop recursing?

   - Smallest valid input
   - Edge cases (empty, zero, one element)

2. **Recursive Case**: How to break down the problem?

   - Must make progress toward base case
   - Problem should get "smaller" each call

3. **Return Value**: What does each call return?

   - How do you combine results from recursive calls?

4. **Trust the Recursion**: Assume recursive call works correctly
   - Focus on one level at a time

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 509, LC 231)
- [ ] Hand-drawn recursion tree for Fibonacci(5)
- [ ] Recursion checklist: base case, recursive case, return value

## Validation

How to verify you completed the work:

- Both solutions accepted
- Recursion tree shows all calls for fib(5)
- Can explain why base case prevents infinite recursion

## Success Criteria

- [ ] Understand base case necessity (prevents infinite recursion)
- [ ] Can trace through recursive calls step by step
- [ ] Can draw recursion trees
- [ ] Identify when recursion leads to repeated work

## Common Pitfalls

- **Missing base case**: Causes infinite recursion / stack overflow
- **Base case never reached**: Recursive call doesn't make progress
- **Not trusting the recursion**: Trying to trace every call mentally
- **Wrong return value combination**: Not properly combining subproblem results

## Next Steps

Tomorrow you'll work on: **Day 9 - Binary Trees: Traversals** - inorder, preorder, postorder

## Social Post Template

"Day 8/31 DSA: Recursion = function calling itself with simpler input. Drew my first recursion tree. Makes the magic visible! #100DaysOfCode #Recursion"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
