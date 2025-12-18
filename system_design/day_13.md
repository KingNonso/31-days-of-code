# Day 13: Design Notification System

## Overview

**Topic**: Real-time notification delivery at scale
**Estimated Time**: 60 minutes
**Difficulty**: Intermediate

## Prerequisites

- Day 12 completed
- Understanding of push notifications
- Message queue knowledge

## Time Breakdown

- **Design (45 min)**: Complete notification system
- **Review (15 min)**: Analyze trade-offs

## The Problem

Design a notification system that can send push notifications, emails, and SMS to millions of users.

## Design Process

### R - Requirements (5 min)

**Functional**:

- Send push notifications (iOS, Android, Web)
- Send emails
- Send SMS
- User notification preferences
- Rate limiting per user

**Non-Functional**:

- 100M daily notifications
- Soft real-time (< 5 seconds for push)
- High reliability (no lost notifications)
- Scalable to 10x growth

### E - Estimations (5 min)

**Volume**:

- 100M notifications/day
- Peak: 10x average = ~12K notifications/second
- Average: ~1,200 notifications/second

**Storage**:

- Notification record: ~500 bytes
- 100M × 500 bytes = 50GB/day
- 30 days retention = 1.5TB

### S - Storage Schema (5 min)

**Notifications Table**:
| Column | Type |
|--------|------|
| notification_id | uuid (PK) |
| user_id | bigint |
| type | enum (push, email, sms) |
| content | jsonb |
| status | enum (pending, sent, failed) |
| created_at | timestamp |
| sent_at | timestamp |

**User Preferences Table**:
| Column | Type |
|--------|------|
| user_id | bigint (PK) |
| push_enabled | boolean |
| email_enabled | boolean |
| sms_enabled | boolean |
| quiet_hours_start | time |
| quiet_hours_end | time |

**Device Tokens Table**:
| Column | Type |
|--------|------|
| user_id | bigint |
| device_token | varchar |
| platform | enum (ios, android, web) |
| updated_at | timestamp |

### H - High-Level Design (10 min)

**Components**:

1. **Notification Service**: Entry point, validates requests
2. **Preference Service**: User settings
3. **Priority Queue**: Message queue with priorities
4. **Workers**: Process and send notifications
5. **Vendor Adapters**: APNS, FCM, Twilio, SendGrid
6. **Analytics Service**: Track delivery, opens

**Flow**:

```
Trigger → Notification Service → Preference Check
→ Priority Queue → Worker → Vendor → User
```

### A - API Design (5 min)

**Send Notification**:

```
POST /notifications
{
  "user_ids": [123, 456],
  "type": "push",
  "priority": "high",
  "content": {
    "title": "New message",
    "body": "You have a new message from John"
  },
  "data": {
    "deep_link": "/messages/789"
  }
}
→ 202 Accepted
{
  "notification_ids": ["abc", "def"]
}
```

**Get User Preferences**:

```
GET /users/{user_id}/notification-preferences
→ {
  "push_enabled": true,
  "email_enabled": true,
  "quiet_hours": { "start": "22:00", "end": "08:00" }
}
```

### D - Detailed Design (10 min)

**Priority Queue Design**:

- High priority: Direct messages, security alerts
- Medium priority: Social interactions
- Low priority: Marketing, digest

**Worker Processing**:

1. Pull from queue
2. Check user preferences
3. Check rate limits
4. Format for vendor
5. Send to vendor API
6. Handle response (retry on failure)
7. Update notification status

**Reliability Mechanisms**:

- At-least-once delivery
- Exponential backoff retry
- Dead letter queue for failures
- Idempotency keys prevent duplicates

**Rate Limiting**:

- Per user: Max 100 notifications/hour
- Per type: Max 10 SMS/day
- Global: Max 1M/minute

### E - Evaluate (5 min)

**Scalability**:

- Horizontal scaling of workers
- Queue partitioning by user_id
- Separate queues per vendor

**Reliability**:

- Retry failed sends
- Monitor vendor health
- Fallback (push fails → email)

**Bottlenecks**:

- Vendor API rate limits
- Queue processing at peak
- Database writes

## Tasks

### Task 1: Draw Complete Architecture (10 min)

Include all components and data flows.

### Task 2: Design Retry Strategy (5 min)

| Attempt | Delay | Action on Failure |
| ------- | ----- | ----------------- |
| 1       | 0     |                   |
| 2       |       |                   |
| 3       |       |                   |
| Final   |       |                   |

### Task 3: Analytics Design (5 min)

What metrics to track:

- ***
- ***
- ***

## Output Requirements

- [ ] Complete architecture designed
- [ ] Queue and worker design documented
- [ ] Retry strategy defined
- [ ] Analytics metrics identified

## Success Criteria

- [ ] Can handle 12K notifications/second
- [ ] Notifications delivered in <5 seconds
- [ ] No lost notifications
- [ ] User preferences respected

## Next Steps

Tomorrow: **Day 14 - Week 2 Review** - Design a Chat System

## Social Post Template

"Day 13/31 System Design: Notification system! Push, email, SMS at 100M/day scale. Priority queues, retry with backoff, rate limiting. Real-time delivery is hard! #SystemDesign #Notifications"

## Notes

_Your personal observations and diagrams go here._

---
