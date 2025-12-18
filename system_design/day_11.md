# Day 11: Microservices Architecture

## Overview

**Topic**: Breaking down monoliths into services
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 10 completed (API design)
- Understanding of monolithic architecture
- Basic distributed systems knowledge

## Time Breakdown

- **Learn (20 min)**: Microservices concepts
- **Practice (30 min)**: Service decomposition
- **Reflect (10 min)**: Trade-off analysis

## Microservices Concepts

### Monolith vs Microservices

**Monolith**:

- Single deployable unit
- Shared database
- Simple to start
- Hard to scale parts independently

**Microservices**:

- Independent services
- Own databases (ideally)
- Complex to manage
- Scale services independently

### When to Use Microservices

✅ Large teams needing independence
✅ Different scaling requirements
✅ Different technology needs
✅ Complex domain boundaries

❌ Small teams
❌ Simple applications
❌ Tight deadlines
❌ Unclear domain boundaries

### Service Communication

**Synchronous**:

- REST/HTTP
- gRPC
- Direct, blocking

**Asynchronous**:

- Message queues
- Event streaming
- Decoupled, non-blocking

### Service Discovery

How services find each other:

- **Client-side**: Client queries registry (Eureka)
- **Server-side**: Load balancer queries registry
- **DNS-based**: Services registered in DNS

### API Gateway

Single entry point that:

- Routes requests to services
- Handles authentication
- Rate limiting
- Request aggregation

### Common Patterns

**Circuit Breaker**: Fail fast when service is down
**Retry with Backoff**: Retry with increasing delays
**Bulkhead**: Isolate failures
**Saga**: Distributed transactions

## Tasks

### Task 1: Decompose URL Shortener (15 min)

Break monolith into services:

**Service 1: URL Service**

- Responsibility: ******\_\_\_******
- Database: ******\_\_\_******
- API endpoints: ******\_\_\_******

**Service 2: Redirect Service**

- Responsibility: ******\_\_\_******
- Database: ******\_\_\_******
- API endpoints: ******\_\_\_******

**Service 3: Analytics Service**

- Responsibility: ******\_\_\_******
- Database: ******\_\_\_******
- API endpoints: ******\_\_\_******

### Task 2: Service Communication (10 min)

Design how services communicate:

| From        | To          | Method | Why |
| ----------- | ----------- | ------ | --- |
| Redirect    | Analytics   |        |     |
| API Gateway | URL Service |        |     |
| URL Service | Cache       |        |     |

### Task 3: Draw Microservices Architecture (10 min)

Draw complete architecture showing:

- API Gateway
- Individual services
- Databases (per service)
- Message queue
- Service discovery

### Task 4: Failure Handling (10 min)

What happens when:

**Analytics service is down**:

- Impact: ******\_\_\_******
- Mitigation: ******\_\_\_******

**URL service is slow**:

- Impact: ******\_\_\_******
- Mitigation: ******\_\_\_******

**Database connection pool exhausted**:

- Impact: ******\_\_\_******
- Mitigation: ******\_\_\_******

## Output Requirements

- [ ] Services decomposed with responsibilities
- [ ] Communication patterns defined
- [ ] Architecture diagram drawn
- [ ] Failure scenarios handled

## Validation

- Are services truly independent?
- Can services be deployed separately?
- Is communication pattern appropriate?

## Success Criteria

- [ ] Understand when to use microservices
- [ ] Can decompose monolith into services
- [ ] Know communication patterns
- [ ] Understand failure handling patterns

## Common Pitfalls

- **Distributed monolith**: Tightly coupled services
- **Too many services**: Start with fewer, split later
- **Shared database**: Each service should own its data
- **No service contracts**: APIs should be versioned

## Next Steps

Tomorrow: **Day 12 - Design: Twitter Feed** - First complete system design

## Social Post Template

"Day 11/31 System Design: Microservices! Decomposed URL shortener into URL, Redirect, and Analytics services. Key: services should be independently deployable. #SystemDesign #Microservices"

## Notes

_Your personal observations and diagrams go here._

---
