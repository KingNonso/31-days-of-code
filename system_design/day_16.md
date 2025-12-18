# Day 16: Design Rate Limiter

## Overview

**Topic**: Protecting services from abuse and overload
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 15 completed
- Understanding of API design
- Basic algorithms knowledge

## Time Breakdown

- **Learn (20 min)**: Rate limiting algorithms
- **Design (30 min)**: Complete rate limiter
- **Reflect (10 min)**: Algorithm comparison

## Rate Limiting Algorithms

### Token Bucket

- Bucket holds tokens (max capacity)
- Tokens added at fixed rate
- Request consumes token
- No token = rejected

**Pros**: Allows bursts, smooth rate
**Cons**: Memory for each bucket

### Leaky Bucket

- Requests enter bucket
- Processed at fixed rate
- Overflow rejected

**Pros**: Smooth output rate
**Cons**: No bursts allowed

### Fixed Window

- Count requests in time window
- Reset at window boundary
- Reject if over limit

**Pros**: Simple, memory efficient
**Cons**: Burst at boundaries

### Sliding Window Log

- Store timestamp of each request
- Count requests in sliding window
- Reject if over limit

**Pros**: Accurate
**Cons**: Memory intensive

### Sliding Window Counter

- Hybrid of fixed and sliding
- Weighted average of windows

**Pros**: Memory efficient, accurate
**Cons**: Approximation

## Design: Distributed Rate Limiter

### Requirements

- 1M+ users
- Multiple rate limit rules
- Distributed (multiple servers)
- Low latency (<10ms overhead)

### Architecture

1. **Rate Limiter Service**: Core logic
2. **Rules Engine**: Define limits
3. **Counter Store**: Redis/Memcached
4. **API Gateway Integration**: Enforcement point

### Tasks

### Task 1: Algorithm Selection (10 min)

| Use Case               | Algorithm | Why |
| ---------------------- | --------- | --- |
| API rate limiting      |           |     |
| DDoS protection        |           |     |
| User quota (daily)     |           |     |
| Smooth traffic shaping |           |     |

### Task 2: Design Rate Limiter (20 min)

**Data Model**:

```
Key: user:{user_id}:endpoint:{endpoint}
Value: {count, window_start}
TTL: window_size
```

**Algorithm** (Token Bucket):

```python
def is_allowed(user_id, endpoint):
    key = f"user:{user_id}:endpoint:{endpoint}"
    # Your logic here
    pass
```

**Distributed Considerations**:

- How to sync counters across servers?
- Race conditions?
- What if Redis is down?

### Task 3: Response Design (10 min)

What to return when rate limited:

**HTTP Response**:

- Status: \_\_\_
- Headers: \_\_\_
- Body: \_\_\_

**Retry-After Logic**:

---

### Task 4: Rules Configuration (10 min)

Design rule schema:

```yaml
rules:
  - name: api_default
    endpoint: "*"
    limit: ___
    window: ___
  - name: auth_strict
    endpoint: "/login"
    limit: ___
    window: ___
```

## Output Requirements

- [ ] Algorithm selected for each use case
- [ ] Rate limiter designed with Redis
- [ ] Response format defined
- [ ] Rules configuration created

## Success Criteria

- [ ] Understand rate limiting algorithms
- [ ] Can design distributed rate limiter
- [ ] Know trade-offs of each algorithm
- [ ] Can configure flexible rules

## Next Steps

Tomorrow: **Day 17 - Design: Distributed Cache** - Redis architecture

## Social Post Template

"Day 16/31 System Design: Rate Limiter deep dive! Token bucket, leaky bucket, sliding window. Designed distributed rate limiter with Redis. Protecting APIs one request at a time. #SystemDesign #RateLimiting"

## Notes

_Your personal observations go here._

---
