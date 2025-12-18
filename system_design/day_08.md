# Day 8: Content Delivery Networks (CDN)

## Overview

**Topic**: Edge caching for global performance
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 7 completed (Week 1 review)
- Understanding of caching concepts
- Basic networking knowledge

## Time Breakdown

- **Learn (20 min)**: CDN concepts
- **Practice (30 min)**: CDN design exercises
- **Reflect (10 min)**: Use case analysis

## CDN Concepts

### What is a CDN?

A geographically distributed network of servers that cache content closer to users.

### How CDNs Work

1. User requests content
2. Request routed to nearest edge server
3. If cached (hit): Return immediately
4. If not cached (miss): Fetch from origin, cache, return

### CDN Benefits

- **Lower latency**: Content served from nearby servers
- **Reduced origin load**: Edge servers handle most requests
- **High availability**: Multiple edge locations
- **DDoS protection**: Distributed traffic absorption

### What to Cache on CDN

- Static assets (images, CSS, JS)
- Video/audio files
- HTML pages (with care)
- API responses (with short TTL)

### CDN Providers

- Cloudflare
- AWS CloudFront
- Akamai
- Fastly

### Cache Invalidation

- **TTL-based**: Content expires after time
- **Purge**: Manually remove specific content
- **Versioning**: Change URL for new versions (app.v2.js)

## Tasks

### Task 1: CDN Architecture Design (15 min)

Add CDN to URL shortener:

**What to cache on CDN**:

- ***

**What NOT to cache**:

- ***

**Draw architecture**:

- Show CDN placement
- Show cache hit flow
- Show cache miss flow

### Task 2: Cache Configuration (10 min)

Define caching rules:

| Content Type       | TTL | Cache-Control Header |
| ------------------ | --- | -------------------- |
| Static images      |     |                      |
| CSS/JS files       |     |                      |
| HTML pages         |     |                      |
| API responses      |     |                      |
| Redirect responses |     |                      |

### Task 3: Global Distribution Design (10 min)

Your URL shortener needs to serve users globally:

**Edge locations needed** (pick 5-10):

- ***

**Origin server location**:

- ***

**Latency comparison**:

- Without CDN (US user to Asia origin): ~200ms
- With CDN (US user to US edge): ~20ms

### Task 4: CDN Selection (10 min)

Compare CDN options:

| Feature        | CloudFront | Cloudflare | Fastly |
| -------------- | ---------- | ---------- | ------ |
| Pricing model  |            |            |        |
| Edge locations |            |            |        |
| Purge speed    |            |            |        |
| Best for       |            |            |        |

**Your choice for URL shortener**: ******\_\_\_******
**Why**: ******\_\_\_******

## Output Requirements

- [ ] CDN architecture designed
- [ ] Caching rules defined
- [ ] Global distribution planned
- [ ] CDN provider selected

## Validation

- Do you know what to cache vs not cache?
- Can you design CDN into system?
- Do you understand cache invalidation?

## Success Criteria

- [ ] Understand CDN benefits
- [ ] Know what to cache on CDN
- [ ] Can design CDN architecture
- [ ] Understand invalidation strategies

## Common Pitfalls

- **Caching dynamic content**: Be careful with personalized content
- **Long TTLs for changing content**: Hard to update
- **Ignoring cache headers**: Origin must send proper headers
- **Not planning invalidation**: How do you update?

## Next Steps

Tomorrow: **Day 9 - Message Queues** - Asynchronous processing

## Social Post Template

"Day 8/31 System Design: CDNs for global scale. Edge caching reduces latency from 200ms to 20ms. Designed global distribution for URL shortener. #SystemDesign #CDN"

## Notes

_Your personal observations and diagrams go here._

---
