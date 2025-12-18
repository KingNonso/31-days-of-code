# Day 27: Design Distributed ID Generator

## Overview

**Topic**: Generating unique IDs at scale
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 26 completed
- Understanding of distributed systems
- Binary/bit manipulation basics

## Time Breakdown

- **Learn (20 min)**: ID generation strategies
- **Design (30 min)**: Build Snowflake-like system
- **Reflect (10 min)**: Trade-off analysis

## ID Generation Strategies

### Requirements for Distributed IDs

- **Unique**: No collisions across all nodes
- **Ordered**: Roughly time-sortable
- **Scalable**: High throughput
- **Available**: No single point of failure

### Common Approaches

**UUID**:

- 128 bits, globally unique
- No coordination needed
- Not sortable, not compact

**Database Auto-Increment**:

- Simple, ordered
- Single point of failure
- Doesn't scale well

**Database Ticket Server**:

- Multiple DBs with different ranges
- Node 1: 1, 3, 5... Node 2: 2, 4, 6...
- Coordination overhead

**Snowflake ID** (Twitter):

- 64 bits total
- Time + Machine ID + Sequence
- Sortable, distributed, fast

## Snowflake ID Design

### Structure (64 bits)

```
| 1 bit | 41 bits    | 10 bits   | 12 bits  |
| sign  | timestamp  | machine   | sequence |
```

- **Sign bit**: Always 0 (positive)
- **Timestamp**: Milliseconds since epoch (69 years)
- **Machine ID**: 1024 machines max
- **Sequence**: 4096 IDs per ms per machine

### Capacity

- Per machine: 4096 IDs/ms = 4M IDs/sec
- Total: 4M × 1024 = 4B IDs/sec

## Tasks

### Task 1: Implement Snowflake (15 min)

Design the ID generation logic:

```python
class SnowflakeGenerator:
    def __init__(self, machine_id):
        self.machine_id = machine_id
        self.sequence = 0
        self.last_timestamp = -1
        self.epoch = 1609459200000  # Jan 1, 2021

    def generate(self):
        timestamp = current_time_ms()

        if timestamp == self.last_timestamp:
            self.sequence = (self.sequence + 1) & 0xFFF
            if self.sequence == 0:
                # Wait for next millisecond
                timestamp = wait_next_ms(self.last_timestamp)
        else:
            self.sequence = 0

        self.last_timestamp = timestamp

        id = ((timestamp - self.epoch) << 22) | \
             (self.machine_id << 12) | \
             self.sequence
        return id
```

### Task 2: Machine ID Assignment (10 min)

How to assign unique machine IDs:

**Options**:

1. Manual configuration
2. Zookeeper coordination
3. Database registry
4. MAC address hash

**Your approach**: ******\_\_\_******

**Handling machine ID exhaustion**: ******\_\_\_******

### Task 3: Clock Skew Handling (10 min)

**Problem**: System clock can go backward

**Solutions**:

- Reject if clock goes back
- Wait until clock catches up
- Use logical clocks

**Your approach**: ******\_\_\_******

### Task 4: Service Architecture (10 min)

**Options**:

**Embedded library**:

- Each service generates locally
- Fast, no network call
- Need machine ID coordination

**Centralized service**:

- Dedicated ID service
- Batch allocation
- Network overhead

**Hybrid**:

- Service allocates ranges
- Local generation within range

**Draw architecture**: ******\_\_\_******

### Task 5: Alternative Designs (5 min)

**ULID** (Universally Unique Lexicographically Sortable ID):

- 128 bits
- Timestamp + randomness
- Lexicographically sortable
- No coordination

**When to use what**:
| Need | Best Choice |
|------|-------------|
| Database-friendly | |
| No coordination | |
| Maximum throughput | |
| URL-safe | |

## Output Requirements

- [ ] Snowflake algorithm implemented
- [ ] Machine ID strategy defined
- [ ] Clock skew handling designed
- [ ] Service architecture chosen
- [ ] Alternative analysis done

## Success Criteria

- [ ] Understand Snowflake design
- [ ] Can implement ID generation
- [ ] Know trade-offs of approaches
- [ ] Can handle edge cases

## Next Steps

Tomorrow: **Day 28 - Week 4 Review** - Design a Search Engine

## Social Post Template

"Day 27/31 System Design: Distributed ID Generator! Snowflake: 64 bits = timestamp + machine + sequence. 4M IDs/sec per machine. Clock skew is the tricky part! #SystemDesign #DistributedSystems"

## Notes

_Your personal observations go here._

---
