# Day 4: Caching Fundamentals

## Overview

**Topic**: Using caches to improve performance
**Estimated Time**: 60 minutes
**Difficulty**: Beginner

## Prerequisites

- Days 1-3 completed
- Understanding of latency concepts
- Basic database knowledge

## Time Breakdown

- **Learn (20 min)**: Caching concepts
- **Practice (30 min)**: Caching design
- **Reflect (10 min)**: Cache strategy selection

## Caching Concepts

### Why Cache?

- RAM access: ~100 ns
- SSD access: ~150 μs
- Network DB query: ~1-10 ms

Caching can provide **100-1000x** speedup.

### Cache Levels

1. **Browser cache**: Client-side, HTTP headers
2. **CDN cache**: Edge servers, static content
3. **Application cache**: In-process memory
4. **Distributed cache**: Redis, Memcached
5. **Database cache**: Query cache, buffer pool

### Caching Strategies

**Cache-Aside (Lazy Loading)**:

```
Read:
1. Check cache
2. If miss, read from DB
3. Update cache
4. Return data

Write:
1. Write to DB
2. Invalidate cache
```

**Write-Through**:

```
Write:
1. Write to cache
2. Cache writes to DB
3. Return success
```

**Write-Behind (Write-Back)**:

```
Write:
1. Write to cache
2. Return success
3. Cache writes to DB asynchronously
```

### Cache Eviction Policies

- **LRU (Least Recently Used)**: Remove oldest accessed
- **LFU (Least Frequently Used)**: Remove least accessed
- **FIFO**: First in, first out
- **TTL (Time To Live)**: Expire after duration

### Common Cache Problems

**Cache Stampede**:

- Many requests hit DB when cache expires
- Solution: Lock, staggered TTL

**Cache Penetration**:

- Queries for non-existent data always hit DB
- Solution: Cache null results, bloom filter

**Cache Inconsistency**:

- Cache and DB out of sync
- Solution: Proper invalidation, short TTL

## Tasks

### Task 1: Caching Strategy Selection (15 min)

Choose the best strategy for each:

**Scenario 1**: User profile data (read-heavy, rarely changes)

- Strategy: ******\_\_\_******
- Why: ******\_\_\_******

**Scenario 2**: Real-time stock prices

- Strategy: ******\_\_\_******
- Why: ******\_\_\_******

**Scenario 3**: E-commerce shopping cart

- Strategy: ******\_\_\_******
- Why: ******\_\_\_******

**Scenario 4**: Social media news feed

- Strategy: ******\_\_\_******
- Why: ******\_\_\_******

### Task 2: Add Caching to URL Shortener (15 min)

Design caching layer:

**What to cache**:

- ***

**Cache strategy**:

- ***

**TTL**:

- ***

**Eviction policy**:

- ***

**Draw updated architecture**:

- Show where cache sits
- Show cache hit vs miss flow

### Task 3: Cache Sizing Calculation (10 min)

For URL shortener:

- 100M URLs total
- 80% of traffic to 20% of URLs (Pareto)
- Each URL entry: 500 bytes

**Questions**:

1. How much cache for top 20% URLs?
2. With 16GB Redis, what % can you cache?
3. Expected cache hit rate?

**Your calculations**:

---

### Task 4: Cache Problem Solutions (10 min)

How would you solve:

**Cache stampede on popular URL expiring**:

---

**Someone requesting non-existent short URLs repeatedly**:

---

**Cache showing old URL after update**:

---

## Output Requirements

- [ ] 4 caching strategies selected with reasoning
- [ ] URL shortener caching layer designed
- [ ] Cache sizing calculated
- [ ] Cache problem solutions documented

## Validation

- Can you explain cache-aside vs write-through?
- Do you know when to use each eviction policy?
- Can you calculate cache size needs?

## Success Criteria

- [ ] Understand caching strategies
- [ ] Know eviction policies
- [ ] Can add caching to designs
- [ ] Know common problems and solutions

## Common Pitfalls

- **Caching everything**: Only cache hot data
- **Long TTLs**: Increases inconsistency risk
- **Ignoring invalidation**: Stale data is often worse than slow data
- **Single cache server**: Need redundancy

## Next Steps

Tomorrow: **Day 5 - Database Fundamentals** - SQL vs NoSQL

## Social Post Template

"Day 4/31 System Design: Caching deep dive. Cache-aside, write-through, write-behind. Calculated cache sizing for URL shortener. 100-1000x speedup is real! #SystemDesign #Caching"

## Notes

_Your personal observations and diagrams go here._

---
