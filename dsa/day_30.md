# Day 30: Mock Interview Prep

## Overview

**Topic**: Timed practice with verbal communication
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Days 1-29 completed
- All patterns mastered
- Ready for interview simulation

## Time Breakdown

- **Problem 1 (35 min)**: Meeting Rooms II with explanation
- **Problem 2 (25 min)**: Longest Palindromic Substring with explanation

## Resources

- [LeetCode 253 - Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) (Premium, or use alternative)
- [LeetCode 5 - Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

## Interview Communication Tips

**Before coding:**

1. Clarify the problem (ask questions)
2. Work through an example
3. Explain your approach
4. Discuss time/space complexity

**While coding:**

1. Talk through your thought process
2. Explain each major step
3. Handle edge cases verbally

**After coding:**

1. Walk through with an example
2. Discuss optimizations
3. Ask if there are questions

## Tasks

### Task 1: Solve Meeting Rooms II (35 min)

- **Problem**: Given intervals, find minimum meeting rooms needed
- **Pattern**: Heap or sweep line

**Talk through it:**
"I'll use a min-heap to track end times of ongoing meetings..."

```python
import heapq

def minMeetingRooms(intervals):
    if not intervals:
        return 0

    # Sort by start time
    intervals.sort(key=lambda x: x[0])

    # Heap stores end times of ongoing meetings
    heap = []

    for start, end in intervals:
        # If earliest ending meeting is done, reuse that room
        if heap and heap[0] <= start:
            heapq.heappop(heap)

        # Add current meeting's end time
        heapq.heappush(heap, end)

    # Heap size = rooms needed
    return len(heap)
```

**Explanation points:**

- Sort by start time to process chronologically
- Heap tracks end times of rooms in use
- If room frees up before new meeting, reuse it
- Final heap size = concurrent meetings = rooms needed

**Time**: O(n log n) for sorting + heap operations
**Space**: O(n) for heap

### Task 2: Solve Longest Palindromic Substring (25 min)

- **Problem**: [LeetCode 5](https://leetcode.com/problems/longest-palindromic-substring/)
- **Pattern**: Expand from center OR DP

**Talk through it:**
"I'll try expand from center approach. For each position, expand outward while palindrome..."

```python
def longestPalindrome(s):
    if len(s) < 2:
        return s

    def expandFromCenter(left, right):
        while left >= 0 and right < len(s) and s[left] == s[right]:
            left -= 1
            right += 1
        return s[left + 1:right]

    result = ""

    for i in range(len(s)):
        # Odd length palindrome (single center)
        odd = expandFromCenter(i, i)
        # Even length palindrome (double center)
        even = expandFromCenter(i, i + 1)

        # Update result if longer found
        if len(odd) > len(result):
            result = odd
        if len(even) > len(result):
            result = even

    return result
```

**Explanation points:**

- Palindrome expands symmetrically from center
- Two cases: odd length (single center) and even length (double center)
- For each position, try both and keep longest

**Time**: O(n²) - n centers, O(n) expansion each
**Space**: O(1) excluding output

### Task 3: Record Yourself (Optional but Recommended)

- Set up recording
- Solve one problem talking out loud
- Review: Did you explain clearly?

### Task 4: Self-Assessment

**Interview Checklist:**

- [ ] Clarified problem before coding?
- [ ] Explained approach before implementation?
- [ ] Talked through code while writing?
- [ ] Handled edge cases?
- [ ] Analyzed complexity?
- [ ] Tested with example?

## Output Requirements

What you must produce today:

- [ ] 2 accepted solutions with time tracking
- [ ] Audio recording or written transcript of explanation
- [ ] Self-assessment using interview checklist

## Validation

How to verify you completed the work:

- Both solutions accepted in time limit
- Can explain each solution clearly
- Communication was organized

## Success Criteria

- [ ] Solved 2 mediums in ~60 min total
- [ ] Explained approach before coding
- [ ] Communicated clearly throughout
- [ ] Handled edge cases

## Common Interview Mistakes

- **Silent coding**: Always talk through your process
- **Jumping to code**: Explain approach first
- **Ignoring edge cases**: Discuss them explicitly
- **Not testing**: Walk through with an example
- **Getting stuck silently**: Think out loud, ask for hints if needed

## Next Steps

Tomorrow you'll work on: **Day 31 - CAPSTONE** - full interview simulation

## Social Post Template

"Day 30/31 DSA: Mock interview day. Talking through solutions out loud is HARD but crucial. Explaining forces clarity. Ready for Day 31 capstone! #100DaysOfCode #InterviewPrep"

## Notes Section

_Use this space for your personal notes, observations, and questions._

---
