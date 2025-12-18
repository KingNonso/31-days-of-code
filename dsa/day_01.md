# Day 1: Two Pointers - Opposite Ends

## Overview

**Topic**: Two pointers moving from both ends of array + Big O analysis
**Estimated Time**: 60 minutes
**Difficulty**: Beginner

## Prerequisites

- Basic understanding of arrays
- Familiarity with any programming language (Python recommended)
- LeetCode account (free tier sufficient)

## Time Breakdown

- **Review (10 min)**: Set up your environment, review array basics
- **Learn (40 min)**: Watch videos + solve 2 problems
- **Reflect (10 min)**: Document pattern and create template code

## Resources

- [NeetCode Two Pointers Intro](https://www.youtube.com/watch?v=cQ1Oz4ckceM) (15 min)
- [Big O Notation Explained - CS Dojo](https://youtu.be/D6xkbGLQeKE) (8 min)
- [Big O Cheat Sheet](https://www.bigocheatsheet.com/)

## Tasks

### Task 1: Learn Big O Fundamentals (10 min)

Watch the Big O video and review the cheat sheet. Understand:

- O(1) - constant time
- O(n) - linear time
- O(n²) - quadratic time
- O(log n) - logarithmic time

### Task 2: Learn Two Pointers Pattern (15 min)

Watch the NeetCode Two Pointers video. Focus on:

- When to use left/right pointers
- How pointers converge toward the middle
- Why this works on sorted arrays

### Task 3: Solve LeetCode 125 - Valid Palindrome (15 min)

- **Problem**: [LeetCode 125](https://leetcode.com/problems/valid-palindrome/)
- **Pattern**: Use left pointer at start, right pointer at end
- **Approach**: Move pointers inward, comparing characters
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

### Task 4: Solve LeetCode 167 - Two Sum II (10 min)

- **Problem**: [LeetCode 167](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- **Pattern**: Left/right pointers on sorted array
- **Approach**: If sum too small, move left pointer right; if too large, move right pointer left
- **Time Complexity**: O(n)
- **Space Complexity**: O(1)

### Task 5: Document Pattern (10 min)

Create a pattern note answering:

- When to use opposite-end two pointers?
- Write template pseudocode
- What makes this O(n) instead of O(n²)?

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions on LeetCode (LC 125, LC 167)
- [ ] Pattern doc: "When to use opposite-end pointers + template code"
- [ ] Written comparison: brute force vs. two-pointer approach with complexity analysis

## Validation

How to verify you completed the work:

- Both solutions show "Accepted" status on LeetCode
- You can explain why two pointers works (convergence logic)
- You understand the space complexity advantage: O(1) vs O(n) hash map

## Success Criteria

- [ ] Can explain O(n), O(n²), O(log n) with examples
- [ ] Solved both problems with optimal time complexity
- [ ] Can recognize when two pointers is applicable
- [ ] Template code written and saved

## Common Pitfalls

- **Forgetting edge cases**: Empty strings, single character
- **Off-by-one errors**: Be careful with pointer bounds
- **Not handling non-alphanumeric characters** in palindrome problems
- **Assuming unsorted arrays**: Two Sum II only works because array is sorted

## Next Steps

Tomorrow you'll work on: **Day 2 - Two Pointers (Same Direction)** - fast/slow pointers for in-place array modification

## Social Post Template

"Day 1/31 DSA: Learned two-pointer pattern. Solved 2 problems using left/right convergence. Key insight: works best on sorted arrays or palindrome checks. #100DaysOfCode #DSA"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
