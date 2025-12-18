# Day 12: Design Twitter/X Feed

## Overview

**Topic**: First complete system design - Social media feed
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Days 1-11 completed
- Understanding of all fundamental concepts
- RESHADED framework mastered

## Time Breakdown

- **Design (45 min)**: Complete Twitter feed design
- **Review (15 min)**: Compare with solutions

## The Problem

Design Twitter/X's home timeline feed showing tweets from people you follow.

## Design Process

### R - Requirements (5 min)

**Functional**:

- Users can post tweets (280 chars)
- Users can follow other users
- Users see feed of tweets from people they follow
- Feed is ordered by time (or relevance)

**Non-Functional**:

- 500M users, 200M daily active
- Average user follows 200 people
- Average user posts 2 tweets/day
- Feed should load in <500ms
- High availability (99.9%)

### E - Estimations (5 min)

**Write (Tweets)**:

- 200M DAU × 2 tweets = 400M tweets/day
- 400M / 86400 = ~4,600 tweets/second

**Read (Feed)**:

- 200M DAU × 10 feed loads = 2B reads/day
- 2B / 86400 = ~23,000 reads/second

**Storage**:

- Tweet: ~500 bytes (text + metadata)
- 400M tweets × 500 bytes = 200GB/day
- 5 years = 365TB

### S - Storage Schema (5 min)

**Users Table**:
| Column | Type |
|--------|------|
| user_id | bigint (PK) |
| username | varchar(50) |
| created_at | timestamp |

**Tweets Table**:
| Column | Type |
|--------|------|
| tweet_id | bigint (PK) |
| user_id | bigint (FK) |
| content | varchar(280) |
| created_at | timestamp |

**Follows Table**:
| Column | Type |
|--------|------|
| follower_id | bigint |
| followee_id | bigint |
| created_at | timestamp |

### H - High-Level Design (10 min)

**Key Components**:

1. **Tweet Service**: Create, read tweets
2. **User Service**: User profiles, authentication
3. **Follow Service**: Manage relationships
4. **Feed Service**: Generate user feeds
5. **Cache Layer**: Redis for hot data
6. **CDN**: Static content, media

**Feed Generation Approaches**:

**Pull Model (Fan-out on read)**:

- When user loads feed, query all followees' tweets
- Pros: No preprocessing, fresh data
- Cons: Slow for users following many people

**Push Model (Fan-out on write)**:

- When tweet posted, push to all followers' feeds
- Pros: Fast reads
- Cons: Slow writes for celebrities, storage heavy

**Hybrid Model** (Best):

- Pull for celebrities (>10K followers)
- Push for regular users

### A - API Design (5 min)

**Post Tweet**:

```
POST /tweets
{
  "content": "Hello world!",
  "media_ids": []
}
→ 201 Created
```

**Get Feed**:

```
GET /feed?limit=20&cursor=abc
→ {
  "tweets": [...],
  "next_cursor": "xyz"
}
```

**Follow User**:

```
POST /users/{user_id}/follow
→ 200 OK
```

### D - Detailed Design (10 min)

**Feed Generation (Hybrid)**:

1. User requests feed
2. Get pre-computed feed from cache (pushed tweets)
3. Get celebrity tweets in real-time (pulled)
4. Merge and sort by time
5. Return to user

**Tweet Posting Flow**:

1. User posts tweet
2. Write to Tweets DB
3. If <10K followers: Fan-out to followers' feeds in cache
4. If ≥10K followers: Do nothing (pulled at read time)
5. Return success

**Caching Strategy**:

- Cache each user's feed (last 800 tweets)
- Cache individual tweets (hot tweets)
- Cache celebrity tweets separately

### E - Evaluate (5 min)

**Bottlenecks**:

- Celebrity tweets at read time
- Cache memory for all feeds
- Database writes at peak times

**Trade-offs**:

- Push vs Pull: Chose hybrid for balance
- Consistency vs Speed: Eventual consistency acceptable
- Storage vs Compute: Heavy caching chosen

## Output Requirements

- [ ] Requirements and estimations documented
- [ ] Storage schema designed
- [ ] High-level architecture drawn
- [ ] API endpoints designed
- [ ] Feed generation algorithm explained

## Validation

- Does your design handle 23K reads/second?
- How does it handle celebrity posts?
- What happens if cache fails?

## Success Criteria

- [ ] Applied RESHADED framework
- [ ] Designed complete system
- [ ] Understood push vs pull trade-off
- [ ] Can explain all decisions

## Next Steps

Tomorrow: **Day 13 - Design: Notification System** - Real-time messaging

## Social Post Template

"Day 12/31 System Design: Designed Twitter Feed! Push for regular users, pull for celebrities (hybrid model). 23K reads/sec, 500ms latency target. RESHADED framework in action! #SystemDesign #TwitterDesign"

## Notes

_Your personal observations and diagrams go here._

---
