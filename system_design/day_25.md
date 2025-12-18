# Day 25: Design E-commerce (Amazon)

## Overview

**Topic**: E-commerce platform at massive scale
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 24 completed
- Understanding of inventory systems
- Payment system knowledge

## Time Breakdown

- **Learn (20 min)**: E-commerce concepts
- **Design (30 min)**: Complete system
- **Reflect (10 min)**: Scale challenges

## E-commerce Concepts

### Key Challenges

- High read traffic (browse)
- Flash sales (sudden spikes)
- Inventory consistency
- Order reliability
- Personalization

### Inventory Management

- **Pessimistic**: Lock inventory during checkout
- **Optimistic**: Check at final step, handle oversell
- **Reservation**: Temporary hold, release if abandoned

### Order States

```
CREATED → PAYMENT_PENDING → PAID → PROCESSING → SHIPPED → DELIVERED
                         ↓
                     CANCELLED
```

## Design: Amazon-Scale E-commerce

### Requirements

- 500M products
- 100M daily active users
- Handle Black Friday (100x traffic)
- 99.99% checkout availability
- Real-time inventory

### Tasks

### Task 1: Product Catalog (10 min)

**Data model**:

```
Product:
  - product_id: uuid
  - title: string
  - description: text
  - price: decimal
  - category_id: uuid
  - seller_id: uuid
  - attributes: jsonb

Inventory:
  - product_id: uuid
  - warehouse_id: uuid
  - quantity: int
  - reserved: int
```

**Search**:

- Elasticsearch for text search
- Faceted filtering
- Personalized ranking

### Task 2: Shopping Cart (10 min)

**Storage options**:

- Logged in: Database
- Guest: Redis with session ID
- Merge on login

**Data**:

```
Cart:
  - cart_id: uuid
  - user_id: uuid (nullable)
  - items: [{product_id, quantity, price_at_add}]
  - created_at: timestamp
```

### Task 3: Checkout Flow (15 min)

**Steps**:

1. Validate cart items available
2. Reserve inventory
3. Calculate total (discounts, tax, shipping)
4. Process payment
5. Create order
6. Confirm inventory deduction
7. Trigger fulfillment

**Inventory reservation**:

- Reserve for 10 minutes
- Release if abandoned
- Handle race conditions

### Task 4: Order Service (10 min)

**Order saga**:

1. Create order (PENDING)
2. Reserve inventory → rollback: release
3. Process payment → rollback: release inventory
4. Confirm order (CONFIRMED)
5. Async: trigger fulfillment, notifications

**Compensation on failure**:

- Payment failed → release inventory
- Inventory unavailable → refund payment

### Task 5: Flash Sale Handling (5 min)

**Challenges**:

- 100x normal traffic
- Limited inventory
- Fair access

**Solutions**:

- Queue-based checkout
- Pre-warm caches
- Rate limiting per user
- CDN for static content

## Output Requirements

- [ ] Product catalog designed
- [ ] Cart storage planned
- [ ] Checkout flow with saga
- [ ] Order state machine
- [ ] Flash sale strategy

## Success Criteria

- [ ] Understand inventory challenges
- [ ] Can design checkout flow
- [ ] Know saga pattern for orders
- [ ] Can handle traffic spikes

## Next Steps

Tomorrow: **Day 26 - Design: Monitoring System** - Observability at scale

## Social Post Template

"Day 25/31 System Design: Amazon E-commerce! 500M products, inventory reservation, checkout saga, flash sale handling. Black Friday ready! #SystemDesign #Ecommerce"

## Notes

_Your personal observations go here._

---
