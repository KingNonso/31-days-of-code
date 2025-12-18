# Day 7: Week 1 Review - Complete URL Shortener Design

## Overview

**Topic**: Integrate all Week 1 concepts into complete system design
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate (Checkpoint)

## Prerequisites

- Days 1-6 completed
- All concepts practiced
- Drawing tools ready

## Time Breakdown

- **Review (15 min)**: Recap all concepts
- **Design (35 min)**: Complete system design
- **Reflect (10 min)**: Self-assessment

## Week 1 Concepts Summary

### Day 1: Fundamentals

- RESHADED framework
- Scale mindset
- Key latency numbers

### Day 2: Scaling

- Vertical vs horizontal
- When to use each
- Trade-offs

### Day 3: Load Balancers

- Algorithms (round robin, least connections, etc.)
- L4 vs L7
- Health checks

### Day 4: Caching

- Strategies (cache-aside, write-through)
- Eviction policies
- Common problems

### Day 5: Databases

- SQL vs NoSQL
- CAP theorem
- When to use which

### Day 6: Database Scaling

- Replication patterns
- Sharding strategies
- Combined approaches

## Complete URL Shortener Design

### Task 1: Requirements (10 min)

**Functional Requirements**:

1. Given long URL, return short URL
2. Given short URL, redirect to long URL
3. Custom short URLs (optional)
4. Analytics (optional)

**Non-Functional Requirements**:

- 100M URLs/month created
- 10:1 read:write ratio
- Low latency (<100ms)
- High availability (99.9%)
- URLs don't expire (or configurable)

**Estimations**:

- Write QPS: ******\_\_\_******
- Read QPS: ******\_\_\_******
- Storage (5 years): ******\_\_\_******
- Bandwidth: ******\_\_\_******

### Task 2: High-Level Design (10 min)

Draw architecture with:

- Clients
- Load balancers
- Application servers
- Cache layer
- Database layer (with replication/sharding)
- CDN (for redirects)

### Task 3: Detailed Component Design (10 min)

**Short URL Generation**:

- Algorithm: ******\_\_\_******
- Length: ******\_\_\_******
- Collision handling: ******\_\_\_******

**Database Schema**:

```
Table: urls
- short_code (PK): _______________
- long_url: _______________
- created_at: _______________
- user_id: _______________
- expires_at: _______________
```

**Caching Strategy**:

- What to cache: ******\_\_\_******
- TTL: ******\_\_\_******
- Eviction: ******\_\_\_******

### Task 4: Scale and Reliability (10 min)

**Scaling Strategy**:

- App servers: ******\_\_\_******
- Database: ******\_\_\_******
- Cache: ******\_\_\_******

**Reliability**:

- What if app server fails?
- What if database master fails?
- What if cache fails?
- What if entire datacenter fails?

### Task 5: Self-Assessment (10 min)

Rate your understanding (1-5):

| Concept            | Rating | Notes |
| ------------------ | ------ | ----- |
| Scale mindset      |        |       |
| Horizontal scaling |        |       |
| Load balancing     |        |       |
| Caching            |        |       |
| Database selection |        |       |
| Database scaling   |        |       |

**Strongest area**: ******\_\_\_******
**Needs more work**: ******\_\_\_******

## Output Requirements

- [ ] Requirements and estimations completed
- [ ] High-level architecture drawn
- [ ] Detailed components designed
- [ ] Scale and reliability addressed
- [ ] Self-assessment completed

## Checkpoint Questions

1. What's the RESHADED framework?
2. When would you choose vertical over horizontal scaling?
3. What load balancing algorithm would you use for stateless servers?
4. What's cache-aside strategy?
5. When would you choose NoSQL over SQL?
6. What's the difference between replication and sharding?

## Success Criteria

- [ ] Can design complete system end-to-end
- [ ] All Week 1 concepts integrated
- [ ] Can explain trade-offs
- [ ] Ready for more complex systems

## Next Steps

Tomorrow: **Day 8 - Content Delivery Networks (CDN)** - Edge caching for global scale

## Social Post Template

"Week 1/31 System Design complete! 🎉 Designed full URL Shortener: load balancers, caching, sharded databases, replication. From 0 to scalable architecture in 7 days. #SystemDesign #Progress"

## Notes

_Your complete URL shortener design goes here._

---
