# Day 9: Message Queues - Asynchronous Processing

## Overview

**Topic**: Decoupling services with message queues
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 8 completed
- Understanding of synchronous vs asynchronous
- Basic distributed systems concepts

## Time Breakdown

- **Learn (20 min)**: Message queue concepts
- **Practice (30 min)**: Queue design exercises
- **Reflect (10 min)**: Use case analysis

## Message Queue Concepts

### What is a Message Queue?

A system that enables asynchronous communication between services by storing messages until they can be processed.

### Why Use Message Queues?

- **Decoupling**: Services don't need to know about each other
- **Load leveling**: Handle traffic spikes gracefully
- **Reliability**: Messages persist if consumer is down
- **Scalability**: Add more consumers as needed

### Queue vs Topic

**Queue (Point-to-Point)**:

- One message → one consumer
- Message deleted after processing
- Use for: Task distribution

**Topic (Pub/Sub)**:

- One message → many subscribers
- Each subscriber gets copy
- Use for: Event broadcasting

### Message Queue Technologies

- **RabbitMQ**: Feature-rich, AMQP protocol
- **Apache Kafka**: High throughput, log-based
- **Amazon SQS**: Managed, simple
- **Redis**: Lightweight, in-memory

### Key Concepts

**Producer**: Creates and sends messages
**Consumer**: Receives and processes messages
**Broker**: Stores and routes messages

**Delivery Guarantees**:

- At-most-once: May lose messages
- At-least-once: May duplicate (common choice)
- Exactly-once: Hard to achieve

### Dead Letter Queue (DLQ)

Messages that fail processing go to DLQ for:

- Manual inspection
- Retry later
- Alerting

## Tasks

### Task 1: Add Queue to URL Shortener (15 min)

Design async processing for analytics:

**Use case**: Track click analytics without slowing redirects

**Architecture**:

- Redirect happens immediately
- Click event sent to queue
- Analytics worker processes asynchronously

**Draw the flow**:

1. User clicks short URL
2. ***
3. ***
4. ***

### Task 2: Queue Configuration (10 min)

Configure your analytics queue:

| Setting            | Value | Reasoning |
| ------------------ | ----- | --------- |
| Delivery guarantee |       |           |
| Message TTL        |       |           |
| Max retries        |       |           |
| DLQ enabled        |       |           |
| Consumer count     |       |           |

### Task 3: Failure Handling (10 min)

What happens when:

**Consumer crashes mid-processing**:

- ***

**Database is down**:

- ***

**Message is malformed**:

- ***

**Queue is full**:

- ***

### Task 4: Queue Selection (10 min)

| Feature     | RabbitMQ | Kafka | SQS |
| ----------- | -------- | ----- | --- |
| Throughput  |          |       |     |
| Ordering    |          |       |     |
| Persistence |          |       |     |
| Complexity  |          |       |     |
| Best for    |          |       |     |

**Your choice**: ******\_\_\_******
**Why**: ******\_\_\_******

## Output Requirements

- [ ] Queue architecture for analytics designed
- [ ] Queue configuration defined
- [ ] Failure scenarios handled
- [ ] Queue technology selected

## Validation

- Do you know when to use queues?
- Can you design async processing?
- Do you understand delivery guarantees?

## Success Criteria

- [ ] Understand message queue benefits
- [ ] Know queue vs topic difference
- [ ] Can design queue-based architecture
- [ ] Understand failure handling

## Common Pitfalls

- **Assuming exactly-once**: Design for at-least-once
- **No DLQ**: Failed messages disappear
- **Blocking on queue**: Queue should be fire-and-forget
- **No monitoring**: Queues need observability

## Next Steps

Tomorrow: **Day 10 - API Design** - RESTful and beyond

## Social Post Template

"Day 9/31 System Design: Message queues for async processing. Decoupling, load leveling, reliability. Added analytics queue to URL shortener - redirects stay fast! #SystemDesign #MessageQueues"

## Notes

_Your personal observations and diagrams go here._

---
