# Day 6: Database Scaling - Replication and Sharding

## Overview

**Topic**: Scaling databases through replication and sharding
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 5 completed (database fundamentals)
- Understanding of consistency concepts
- Basic distributed systems knowledge

## Time Breakdown

- **Learn (20 min)**: Replication and sharding concepts
- **Practice (30 min)**: Design exercises
- **Reflect (10 min)**: Strategy selection

## Database Replication

### What is Replication?

Copying data across multiple database servers for:

- High availability
- Read scalability
- Geographic distribution

### Replication Patterns

**Single Leader (Master-Slave)**:

- One master handles writes
- Multiple replicas handle reads
- Replicas sync from master

Pros: Simple, read scalability
Cons: Write bottleneck, single point of failure

**Multi-Leader**:

- Multiple masters accept writes
- Masters sync with each other
- Good for multi-datacenter

Pros: Write availability, geographic distribution
Cons: Conflict resolution complex

**Leaderless**:

- Any node accepts reads/writes
- Quorum-based consistency
- Examples: Cassandra, DynamoDB

Pros: High availability
Cons: Complex consistency

### Replication Lag

Time between master write and replica sync:

- Synchronous: Wait for replicas (slower, consistent)
- Asynchronous: Don't wait (faster, eventual consistency)

## Database Sharding (Partitioning)

### What is Sharding?

Splitting data across multiple databases based on shard key.

### Sharding Strategies

**Range-Based**:

- Users A-M → Shard 1
- Users N-Z → Shard 2

Pros: Range queries efficient
Cons: Hotspots possible

**Hash-Based**:

- hash(user_id) % N → Shard number

Pros: Even distribution
Cons: Range queries across shards

**Directory-Based**:

- Lookup service maps key → shard

Pros: Flexible
Cons: Lookup overhead, single point of failure

### Sharding Challenges

- **Cross-shard queries**: Expensive
- **Transactions**: Distributed transactions complex
- **Rebalancing**: Adding shards requires data migration
- **Hotspots**: Uneven data distribution

## Tasks

### Task 1: Replication Design (15 min)

Design replication for URL shortener:

**Pattern choice**: ******\_\_\_******

**Number of replicas**: ******\_\_\_******

**Sync strategy**: ******\_\_\_******

**How reads are handled**:

---

**How writes are handled**:

---

**What happens if master fails**:

---

### Task 2: Sharding Design (15 min)

Design sharding for URL shortener at 1 billion URLs:

**Shard key**: ******\_\_\_******

**Sharding strategy**: ******\_\_\_******

**Number of shards** (justify):

---

**How to find which shard has a URL**:

---

**How to handle a new shard addition**:

---

### Task 3: Combined Architecture (10 min)

Draw complete database architecture:

- Multiple shards
- Each shard replicated
- Show read/write paths
- Show failover scenario

### Task 4: Trade-off Analysis (10 min)

| Approach                  | Pros | Cons | Best For |
| ------------------------- | ---- | ---- | -------- |
| Single leader replication |      |      |          |
| Multi-leader replication  |      |      |          |
| Hash-based sharding       |      |      |          |
| Range-based sharding      |      |      |          |

## Output Requirements

- [ ] Replication design completed
- [ ] Sharding design completed
- [ ] Combined architecture drawn
- [ ] Trade-off analysis done

## Validation

- Can you explain replication patterns?
- Do you know sharding strategies?
- Can you design scaled database architecture?

## Success Criteria

- [ ] Understand replication options
- [ ] Know sharding strategies
- [ ] Can design combined approach
- [ ] Understand trade-offs

## Common Pitfalls

- **Wrong shard key**: Causes hotspots
- **Too few shards**: Hard to scale later
- **Ignoring replication lag**: Causes consistency issues
- **Cross-shard operations**: Should be minimized

## Next Steps

Tomorrow: **Day 7 - Week 1 Review** - Design a complete system

## Social Post Template

"Day 6/31 System Design: Database scaling with replication and sharding. Single-leader, multi-leader, hash vs range sharding. Designed scaled DB architecture for URL shortener. #SystemDesign #DatabaseScaling"

## Notes

_Your personal observations and diagrams go here._

---
