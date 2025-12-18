# Day 21: Week 3 Review - Design Web Crawler

## Overview

**Topic**: Week 3 checkpoint - Design a web crawler
**Estimated Time**: 60 minutes
**Difficulty**: Advanced (Checkpoint)

## Prerequisites

- Days 15-20 completed
- All Week 3 concepts mastered
- Ready for full design exercise

## Time Breakdown

- **Review (10 min)**: Recap Week 3
- **Design (40 min)**: Complete web crawler
- **Reflect (10 min)**: Self-assessment

## Week 3 Concepts Summary

### Day 15: Consistency Patterns

- Strong vs eventual consistency
- Conflict resolution

### Day 16: Rate Limiter

- Token bucket, sliding window
- Distributed rate limiting

### Day 17: Distributed Cache

- Consistent hashing
- Replication strategies

### Day 18: Search Autocomplete

- Trie data structures
- Ranking and personalization

### Day 19: Video Streaming

- Transcoding pipeline
- Adaptive bitrate

### Day 20: Ride Sharing

- Geospatial indexing
- Real-time matching

## Design Challenge: Web Crawler (Google Scale)

### Requirements

- Crawl 1 billion pages/day
- Politeness (respect robots.txt)
- Handle duplicate content
- Distributed across many machines
- Resume from failures

### Estimations

- 1B pages/day = 11,500 pages/second
- Average page: 500KB
- Daily download: 500TB
- Storage (compressed): ~50TB/day

### Tasks

### Task 1: High-Level Architecture (10 min)

**Components**:

1. **URL Frontier**: Queue of URLs to crawl
2. **Fetcher**: Download pages
3. **Parser**: Extract links, content
4. **Duplicate Detector**: Skip seen content
5. **URL Filter**: robots.txt, blacklist
6. **Storage**: Raw pages, processed data

### Task 2: URL Frontier Design (10 min)

**Requirements**:

- Prioritize important URLs
- Respect crawl delay per domain
- Distribute work across crawlers

**Design**:

```
Priority Queues:
  - High: News sites, frequently updated
  - Medium: Popular sites
  - Low: Long tail

Per-Host Queues:
  - Ensure politeness
  - One request per host at a time
```

### Task 3: Deduplication (10 min)

**URL deduplication**:

- Normalize URLs
- Store in distributed hash set
- Bloom filter for memory efficiency

**Content deduplication**:

- Hash page content (SimHash for near-duplicates)
- Compare before storing

### Task 4: Distributed Crawling (10 min)

**How to distribute**:

- Partition by URL hash
- Each crawler owns subset of domains
- Consistent hashing for assignment

**Coordination**:

- Central coordinator vs peer-to-peer
- Handle crawler failures
- Rebalancing

### Task 5: Self-Assessment (10 min)

Rate understanding (1-5):

| Concept              | Rating | Notes |
| -------------------- | ------ | ----- |
| Consistency patterns |        |       |
| Rate limiting        |        |       |
| Distributed cache    |        |       |
| Autocomplete         |        |       |
| Video streaming      |        |       |
| Location services    |        |       |
| Web crawling         |        |       |

**Strongest area**: ******\_\_\_******
**Needs more work**: ******\_\_\_******

## Output Requirements

- [ ] Web crawler architecture designed
- [ ] URL frontier with priorities
- [ ] Deduplication strategy
- [ ] Distribution approach
- [ ] Self-assessment completed

## Checkpoint Questions

1. When would you choose eventual over strong consistency?
2. Which rate limiting algorithm allows bursts?
3. Why use consistent hashing for distributed cache?
4. How does adaptive bitrate work?
5. How do you efficiently query nearby locations?

## Success Criteria

- [ ] Applied Week 3 concepts
- [ ] Designed complete web crawler
- [ ] Understood all trade-offs
- [ ] Ready for advanced topics

## Next Steps

Tomorrow: **Day 22 - Design: Google Docs** - Real-time collaboration

## Social Post Template

"Week 3/31 System Design complete! 🎉 Designed web crawler: 1B pages/day, distributed crawling, politeness, deduplication. From consistency to location services - foundations strong! #SystemDesign #Progress"

## Notes

_Your complete web crawler design goes here._

---
