# Day 3: Load Balancers

## Overview

**Topic**: Distributing traffic across multiple servers
**Estimated Time**: 60 minutes
**Difficulty**: Beginner

## Prerequisites

- Day 2 completed (horizontal scaling)
- Understanding of HTTP basics
- Basic networking knowledge

## Time Breakdown

- **Learn (20 min)**: Load balancer concepts
- **Practice (30 min)**: Design exercises
- **Reflect (10 min)**: Algorithm comparison

## Load Balancer Concepts

### What is a Load Balancer?

A device/service that distributes incoming traffic across multiple servers to ensure:

- No single server is overwhelmed
- High availability
- Optimal resource utilization

### Load Balancing Algorithms

**Round Robin**:

- Requests distributed sequentially
- Simple, works well for similar servers
- Doesn't consider server load

**Weighted Round Robin**:

- Servers assigned weights based on capacity
- More powerful servers get more requests

**Least Connections**:

- Routes to server with fewest active connections
- Good for varying request durations

**IP Hash**:

- Client IP determines server
- Ensures same client hits same server (sticky sessions)

**Least Response Time**:

- Routes to fastest responding server
- Requires health monitoring

### Layer 4 vs Layer 7 Load Balancing

**Layer 4 (Transport)**:

- Routes based on IP and port
- Faster, less intelligent
- Can't inspect content

**Layer 7 (Application)**:

- Routes based on content (URL, headers, cookies)
- More flexible, slower
- Can make smart routing decisions

### Health Checks

Load balancers monitor server health:

- Active: Periodic pings to servers
- Passive: Monitor response failures
- Remove unhealthy servers from pool

## Tasks

### Task 1: Algorithm Selection (15 min)

Choose the best algorithm for each scenario:

**Scenario 1**: 3 identical web servers, stateless application

- Algorithm: ******\_\_\_******
- Why: ******\_\_\_******

**Scenario 2**: Servers with different capacities (2 powerful, 3 weak)

- Algorithm: ******\_\_\_******
- Why: ******\_\_\_******

**Scenario 3**: Shopping cart that must maintain session state

- Algorithm: ******\_\_\_******
- Why: ******\_\_\_******

**Scenario 4**: Long-running websocket connections

- Algorithm: ******\_\_\_******
- Why: ******\_\_\_******

### Task 2: Design with Load Balancer (15 min)

Add load balancer to your URL shortener:

**Draw architecture showing**:

- Client requests
- Load balancer
- Multiple application servers
- Database layer

**Questions to answer**:

- Layer 4 or Layer 7? Why?
- What algorithm would you use?
- What happens if a server fails?
- How do you handle the database (single point of failure)?

### Task 3: Health Check Design (10 min)

Design health check strategy for your system:

**Health check endpoint**:

- URL: ******\_\_\_******
- What does it check?
- How often?
- What response indicates healthy?

**Failure handling**:

- After how many failures is server removed?
- How is it added back?

### Task 4: Load Balancer Comparison (10 min)

Research and compare:

| Feature       | HAProxy | NGINX | AWS ELB |
| ------------- | ------- | ----- | ------- |
| Type (L4/L7)  |         |       |         |
| Cost          |         |       |         |
| Ease of setup |         |       |         |
| Best for      |         |       |         |

## Output Requirements

- [ ] 4 algorithm selections with reasoning
- [ ] URL shortener with load balancer designed
- [ ] Health check strategy documented
- [ ] Load balancer comparison completed

## Validation

- Can you explain different LB algorithms?
- Do you know when to use L4 vs L7?
- Can you design health check strategy?

## Success Criteria

- [ ] Understand load balancer purpose
- [ ] Know common algorithms and when to use each
- [ ] Can add LB to system design
- [ ] Understand health checks

## Common Pitfalls

- **Forgetting about state**: Sticky sessions complicate scaling
- **Single LB as SPOF**: Need redundant load balancers
- **Wrong algorithm**: Match algorithm to use case
- **Ignoring health checks**: Unhealthy servers should be removed

## Next Steps

Tomorrow: **Day 4 - Caching Fundamentals** - Speeding up with caches

## Social Post Template

"Day 3/31 System Design: Load Balancers! Round Robin, Least Connections, IP Hash - each has its place. Designed health checks and added LB to my URL shortener. #SystemDesign #LoadBalancing"

## Notes

_Your personal observations and diagrams go here._

---
