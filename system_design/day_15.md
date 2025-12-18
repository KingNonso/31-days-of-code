# Day 15: Consistency Patterns

## Overview

**Topic**: Strong vs eventual consistency and when to use each
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 14 completed
- Understanding of CAP theorem
- Distributed systems basics

## Time Breakdown

- **Learn (25 min)**: Consistency concepts
- **Practice (25 min)**: Pattern selection
- **Reflect (10 min)**: Trade-off analysis

## Consistency Concepts

### Strong Consistency

All reads return the most recent write. Every node sees the same data at the same time.

**Pros**: Simple programming model, no stale data
**Cons**: Higher latency, lower availability

**Use when**: Banking, inventory, bookings

### Eventual Consistency

Given enough time, all reads will return the same value. Temporary inconsistency is acceptable.

**Pros**: Higher availability, lower latency
**Cons**: Complex programming, temporary stale data

**Use when**: Social media, analytics, caching

### Consistency Levels

| Level            | Description                      | Example         |
| ---------------- | -------------------------------- | --------------- |
| Strong           | All reads see latest write       | Banking         |
| Causal           | Cause-effect ordering maintained | Comments        |
| Read-your-writes | User sees their own writes       | Profile updates |
| Monotonic reads  | Never see older data than before | News feed       |
| Eventual         | Eventually consistent            | Like counts     |

### Consensus Algorithms

How distributed systems agree on values:

- **Paxos**: Complex but proven
- **Raft**: Easier to understand
- **ZAB**: Used by Zookeeper

## Tasks

### Task 1: Consistency Selection (15 min)

Choose consistency level for each:

| Feature        | Level | Reasoning |
| -------------- | ----- | --------- |
| Bank balance   |       |           |
| Like count     |       |           |
| Shopping cart  |       |           |
| User profile   |       |           |
| Flight booking |       |           |
| News feed      |       |           |

### Task 2: Design Consistent System (15 min)

Design a ticket booking system:

**Requirement**: No double-booking

**Approach**:

- Database: ******\_\_\_******
- Locking strategy: ******\_\_\_******
- Consistency level: ******\_\_\_******
- What happens under high load?

### Task 3: Design Eventually Consistent System (10 min)

Design a like counter:

**Requirement**: Millions of likes/second

**Approach**:

- Write path: ******\_\_\_******
- Read path: ******\_\_\_******
- How stale can data be?
- Trade-offs made: ******\_\_\_******

### Task 4: Conflict Resolution (10 min)

In eventually consistent systems, conflicts happen. How to resolve:

| Strategy        | Description | When to use |
| --------------- | ----------- | ----------- |
| Last-write-wins |             |             |
| Merge           |             |             |
| Custom logic    |             |             |

## Output Requirements

- [ ] Consistency levels selected for 6 features
- [ ] Consistent booking system designed
- [ ] Eventually consistent counter designed
- [ ] Conflict resolution strategies documented

## Success Criteria

- [ ] Understand strong vs eventual consistency
- [ ] Know when to use each level
- [ ] Can design for both patterns
- [ ] Understand conflict resolution

## Next Steps

Tomorrow: **Day 16 - Design: Rate Limiter** - Protecting services from abuse

## Social Post Template

"Day 15/31 System Design: Consistency patterns! Strong for banking, eventual for likes. Designed ticket booking (no double-booking) and like counter (millions/sec). Trade-offs everywhere! #SystemDesign #Consistency"

## Notes

_Your personal observations go here._

---
