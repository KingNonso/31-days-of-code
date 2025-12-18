# Day 2: Horizontal vs Vertical Scaling

## Overview

**Topic**: Understanding scaling strategies and when to use each
**Estimated Time**: 60 minutes
**Difficulty**: Beginner

## Prerequisites

- Day 1 completed
- Understanding of basic server concepts
- Familiarity with load concepts

## Time Breakdown

- **Learn (20 min)**: Scaling concepts
- **Practice (30 min)**: Scaling exercises
- **Reflect (10 min)**: Trade-off analysis

## Scaling Concepts

### Vertical Scaling (Scale Up)

Add more power to existing machine:

- More CPU cores
- More RAM
- Faster storage

**Pros**:

- Simple to implement
- No code changes needed
- No data distribution complexity

**Cons**:

- Hardware limits exist
- Single point of failure
- Expensive at high end
- Downtime during upgrades

### Horizontal Scaling (Scale Out)

Add more machines:

- Multiple servers behind load balancer
- Distributed processing
- Data partitioning

**Pros**:

- Nearly unlimited scaling
- Better fault tolerance
- Cost-effective (commodity hardware)
- No single point of failure

**Cons**:

- More complex architecture
- Data consistency challenges
- Network overhead
- Requires code changes

### When to Use Which?

| Scenario                   | Recommendation    |
| -------------------------- | ----------------- |
| Early stage, low traffic   | Vertical first    |
| Predictable, steady growth | Horizontal        |
| Sudden traffic spikes      | Horizontal        |
| Complex distributed state  | Consider vertical |
| Cost-sensitive at scale    | Horizontal        |

## Tasks

### Task 1: Scaling Scenarios Analysis (15 min)

For each scenario, recommend vertical or horizontal and explain why:

**Scenario 1**: A blog with 1,000 daily visitors expecting 10x growth

- Recommendation: ******\_\_\_******
- Reasoning: ******\_\_\_******

**Scenario 2**: E-commerce site during Black Friday (100x normal traffic)

- Recommendation: ******\_\_\_******
- Reasoning: ******\_\_\_******

**Scenario 3**: Database server running out of memory

- Recommendation: ******\_\_\_******
- Reasoning: ******\_\_\_******

**Scenario 4**: Real-time gaming server needing low latency

- Recommendation: ******\_\_\_******
- Reasoning: ******\_\_\_******

### Task 2: Calculate Scaling Needs (15 min)

Your service handles 1,000 requests/second on one server.

**Questions**:

1. If traffic grows to 10,000 req/sec, how many servers needed (horizontal)?
2. What vertical specs might handle 10,000 req/sec?
3. At 100,000 req/sec, is vertical still viable? Why/why not?

**Your calculations**:

---

### Task 3: Design Scaled Architecture (15 min)

Take your Day 1 URL shortener and show:

**Version 1 (Vertical)**:

- Single powerful server
- Draw architecture
- Identify limits

**Version 2 (Horizontal)**:

- Multiple servers
- Add load balancer
- Consider database scaling
- Draw architecture

### Task 4: Trade-off Documentation (10 min)

Create a comparison table:

| Factor              | Vertical | Horizontal |
| ------------------- | -------- | ---------- |
| Cost at small scale |          |            |
| Cost at large scale |          |            |
| Complexity          |          |            |
| Fault tolerance     |          |            |
| Maximum capacity    |          |            |

## Output Requirements

- [ ] 4 scenarios analyzed with recommendations
- [ ] Scaling calculations completed
- [ ] Two URL shortener architectures drawn
- [ ] Trade-off table completed

## Validation

- Can you explain when to use each scaling type?
- Can you calculate basic scaling needs?
- Do you understand the trade-offs?

## Success Criteria

- [ ] Understand vertical vs horizontal scaling
- [ ] Can recommend appropriate scaling strategy
- [ ] Can draw scaled architectures
- [ ] Know trade-offs for each approach

## Common Pitfalls

- **Over-engineering early**: Start vertical, scale horizontal when needed
- **Ignoring state**: Stateful services are harder to scale horizontally
- **Forgetting database**: App servers scale easier than databases
- **Not planning ahead**: Design for horizontal even if starting vertical

## Next Steps

Tomorrow: **Day 3 - Load Balancers** - Distributing traffic across servers

## Social Post Template

"Day 2/31 System Design: Vertical vs Horizontal scaling. Key insight: Start simple (vertical), design for horizontal. Analyzed 4 scenarios and drew scaled architectures. #SystemDesign #Scaling"

## Notes

_Your personal observations and diagrams go here._

---
