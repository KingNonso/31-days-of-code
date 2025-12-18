# Day 28: Week 4 Review - Design Search Engine

## Overview

**Topic**: Week 4 checkpoint - Design a search engine
**Estimated Time**: 60 minutes
**Difficulty**: Advanced (Checkpoint)

## Prerequisites

- Days 22-27 completed
- All Week 4 concepts mastered
- Ready for complex design

## Time Breakdown

- **Review (10 min)**: Recap Week 4
- **Design (40 min)**: Complete search engine
- **Reflect (10 min)**: Self-assessment

## Week 4 Concepts Summary

### Day 22: Google Docs

- Operational Transformation
- Real-time collaboration
- WebSocket architecture

### Day 23: Dropbox

- File chunking and sync
- Deduplication
- Conflict resolution

### Day 24: Payment System

- Idempotency
- Double-entry ledger
- Failure handling

### Day 25: E-commerce

- Inventory management
- Checkout saga
- Flash sale handling

### Day 26: Monitoring

- Metrics, logs, traces
- Time-series storage
- Alerting

### Day 27: ID Generator

- Snowflake algorithm
- Machine ID coordination
- Clock skew handling

## Design Challenge: Google-Scale Search Engine

### Requirements

- Index 10 billion web pages
- Sub-second search latency
- Handle 100K queries/second
- Ranked results
- Autocomplete

### Estimations

- 10B pages × 100KB avg = 1PB raw data
- Index size: ~300TB
- Query: 100K QPS peak

### Tasks

### Task 1: Indexing Pipeline (15 min)

**Components**:

1. **Web Crawler**: Fetch pages
2. **Parser**: Extract text, links
3. **Indexer**: Build inverted index
4. **Storage**: Store index

**Inverted Index**:

```
Term → [(doc_id, frequency, positions), ...]

"apple" → [
  (doc_1, 5, [10, 50, 100]),
  (doc_2, 2, [20, 80])
]
```

**Design the pipeline flow**

### Task 2: Query Processing (10 min)

**Flow**:

1. Parse query
2. Tokenize and normalize
3. Lookup terms in index
4. Intersect results
5. Rank by relevance
6. Return top K

**Ranking factors**:

- Term frequency (TF)
- Inverse document frequency (IDF)
- PageRank
- Freshness
- Click-through rate

### Task 3: Distributed Architecture (10 min)

**Sharding**:

- By document ID
- By term
- Hybrid

**Your choice**: ******\_\_\_******

**Replication**:

- Each shard replicated N times
- Load balance across replicas

### Task 4: Autocomplete Integration (10 min)

Combine with Day 18 design:

- Trie for prefix matching
- Search history for personalization
- Trending queries

### Task 5: Self-Assessment (10 min)

Rate understanding (1-5):

| Concept                 | Rating | Notes |
| ----------------------- | ------ | ----- |
| Real-time collaboration |        |       |
| File sync               |        |       |
| Payment systems         |        |       |
| E-commerce              |        |       |
| Monitoring              |        |       |
| ID generation           |        |       |
| Search engines          |        |       |

**Strongest area**: ******\_\_\_******
**Needs more work**: ******\_\_\_******

## Output Requirements

- [ ] Indexing pipeline designed
- [ ] Query processing flow
- [ ] Distributed architecture
- [ ] Autocomplete integration
- [ ] Self-assessment completed

## Checkpoint Questions

1. How does OT handle concurrent edits?
2. Why use chunking for file sync?
3. Why is idempotency critical for payments?
4. What is the saga pattern?
5. How does Snowflake generate unique IDs?

## Success Criteria

- [ ] Applied Week 4 concepts
- [ ] Designed complete search engine
- [ ] Understood all trade-offs
- [ ] Ready for final week

## Next Steps

Tomorrow: **Day 29 - Mock Interview Practice** - Full design exercises

## Social Post Template

"Week 4/31 System Design complete! 🎉 Designed search engine: inverted index, 100K QPS, sub-second latency. From docs to payments to search - advanced topics done! #SystemDesign #Progress"

## Notes

_Your complete search engine design goes here._

---
