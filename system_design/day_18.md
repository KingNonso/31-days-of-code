# Day 18: Design Search Autocomplete

## Overview

**Topic**: Type-ahead suggestions at scale
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 17 completed
- Understanding of tries/prefix trees
- Caching knowledge

## Time Breakdown

- **Learn (20 min)**: Autocomplete concepts
- **Design (30 min)**: Complete system
- **Reflect (10 min)**: Optimization strategies

## Autocomplete Concepts

### Data Structures

**Trie (Prefix Tree)**:

- Each node = character
- Path from root = prefix
- Efficient prefix lookups

**Advantages**:

- O(L) lookup (L = query length)
- Space efficient for common prefixes
- Natural ranking by frequency

### Ranking Strategies

- **Frequency**: Most searched
- **Recency**: Recently popular
- **Personalized**: User's history
- **Trending**: Rising searches

### Update Strategies

- **Real-time**: Update on every search
- **Batch**: Periodic updates
- **Hybrid**: Fast path + batch

## Design: Google-Scale Autocomplete

### Requirements

- 5 billion searches/day
- Suggestions in <100ms
- Top 10 suggestions per prefix
- Personalized + global suggestions

### Estimations

- 5B searches/day = 60K searches/sec
- Average query: 4 characters typed
- 60K × 4 = 240K autocomplete requests/sec

### Tasks

### Task 1: Data Structure Design (10 min)

Design trie node:

```
Node:
  - char: character
  - children: map[char]Node
  - is_end: bool
  - top_k: [(term, score), ...]  // cached top results
```

**Storage calculation**:

- 1M unique queries
- Average query length: 15 chars
- Storage needed: \_\_\_

### Task 2: System Architecture (15 min)

**Components**:

1. **Query Service**: Handle autocomplete requests
2. **Trie Service**: Store and search tries
3. **Aggregation Service**: Collect search data
4. **Ranking Service**: Calculate scores

**Data flow**:

1. User types "ho"
2. ***
3. ***
4. Return ["hotel", "house", "horse"]

### Task 3: Caching Strategy (10 min)

**What to cache**:

- Top prefixes (1-3 chars) → hot
- Full trie in memory
- User's recent searches

**Cache layers**:
| Layer | What | TTL |
|-------|------|-----|
| Browser | | |
| CDN | | |
| Application | | |

### Task 4: Update Pipeline (10 min)

**Batch update flow**:

1. Collect search logs
2. Aggregate by prefix
3. Calculate new scores
4. Update trie
5. Invalidate caches

**Frequency**: \_\_\_

### Task 5: Personalization (5 min)

How to personalize suggestions:

- User's search history
- Location
- Time of day
- Merge personal + global scores

## Output Requirements

- [ ] Trie data structure designed
- [ ] System architecture drawn
- [ ] Caching strategy defined
- [ ] Update pipeline designed
- [ ] Personalization approach documented

## Success Criteria

- [ ] Understand trie-based autocomplete
- [ ] Can design at Google scale
- [ ] Know caching strategies
- [ ] Can handle updates and personalization

## Next Steps

Tomorrow: **Day 19 - Design: YouTube/Netflix** - Video streaming at scale

## Social Post Template

"Day 18/31 System Design: Search Autocomplete! Tries for prefix lookup, 240K requests/sec, <100ms latency. Multi-layer caching + personalization. Every keystroke counts! #SystemDesign #Autocomplete"

## Notes

_Your personal observations go here._

---
