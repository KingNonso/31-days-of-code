# Day 14: Week 2 Review - Design Chat System

## Overview

**Topic**: Week 2 checkpoint - Complete chat system design
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate (Checkpoint)

## Prerequisites

- Days 8-13 completed
- All Week 2 concepts mastered
- Ready for full design exercise

## Time Breakdown

- **Review (10 min)**: Recap Week 2 concepts
- **Design (40 min)**: Complete chat system
- **Reflect (10 min)**: Self-assessment

## Week 2 Concepts Summary

### Day 8: CDN

- Edge caching for global performance
- Cache invalidation strategies

### Day 9: Message Queues

- Async processing
- Delivery guarantees

### Day 10: API Design

- REST principles
- Rate limiting

### Day 11: Microservices

- Service decomposition
- Communication patterns

### Days 12-13: Complete Designs

- Twitter feed (push/pull)
- Notification system

## Design Challenge: Chat System (WhatsApp/Messenger)

### R - Requirements

**Functional**:

- 1:1 messaging
- Group chats (up to 500 members)
- Online/offline status
- Read receipts
- Message history

**Non-Functional**:

- 500M daily active users
- 50B messages/day
- Message delivery < 500ms
- 99.99% availability
- Messages stored indefinitely

### E - Estimations

**Calculate**:

- Messages per second: ******\_\_\_******
- Storage per day: ******\_\_\_******
- Storage for 5 years: ******\_\_\_******

### S - Storage Schema

**Design tables for**:

- Users
- Messages
- Conversations
- Group members

### H - High-Level Design

**Components needed**:

1. ***
2. ***
3. ***
4. ***
5. ***

**Key decisions**:

- How to deliver messages in real-time?
- How to handle offline users?
- How to scale group messages?

### A - API Design

**Design endpoints for**:

- Send message
- Get conversation history
- Create group
- Update online status

### D - Detailed Design

**Real-time Messaging**:

- WebSocket vs Long Polling vs SSE?
- Connection management?
- Message ordering?

**Offline Messages**:

- Storage strategy?
- Sync mechanism?
- Push notification trigger?

**Group Messaging**:

- Fan-out strategy?
- How to handle 500 members?

### E - Evaluate

**Trade-offs made**:

1. ***
2. ***
3. ***

**Potential bottlenecks**:

1. ***
2. ***

## Self-Assessment

Rate your understanding (1-5):

| Concept                | Rating | Notes |
| ---------------------- | ------ | ----- |
| CDN                    |        |       |
| Message Queues         |        |       |
| API Design             |        |       |
| Microservices          |        |       |
| Real-time systems      |        |       |
| Complete system design |        |       |

**Strongest area**: ******\_\_\_******
**Needs more work**: ******\_\_\_******

## Output Requirements

- [ ] Complete chat system designed using RESHADED
- [ ] All estimations calculated
- [ ] Architecture diagram drawn
- [ ] Real-time messaging solution chosen
- [ ] Self-assessment completed

## Checkpoint Questions

1. When would you use CDN vs application cache?
2. What delivery guarantee would you use for chat messages?
3. How do you ensure message ordering?
4. How do you handle users with poor connectivity?
5. How do you scale group messaging?

## Success Criteria

- [ ] Applied Week 2 concepts
- [ ] Designed complete real-time system
- [ ] Understood WebSocket architecture
- [ ] Can explain all trade-offs

## Next Steps

Tomorrow: **Day 15 - Consistency Patterns** - Strong vs eventual consistency

## Social Post Template

"Week 2/31 System Design complete! 🎉 Designed full chat system: WebSockets, message queues, offline sync. 500M users, 50B messages/day. Real-time at scale! #SystemDesign #Progress"

## Notes

_Your complete chat system design goes here._

---
