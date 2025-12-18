# Day 24: Design Payment System

## Overview

**Topic**: Financial transactions at scale
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 23 completed
- Understanding of ACID transactions
- Basic security concepts

## Time Breakdown

- **Learn (20 min)**: Payment concepts
- **Design (30 min)**: Complete system
- **Reflect (10 min)**: Security considerations

## Payment System Concepts

### Key Requirements

- **Correctness**: No double charges, no lost payments
- **Security**: Fraud prevention, encryption
- **Compliance**: PCI-DSS, regulations
- **Reliability**: Handle failures gracefully

### Payment Flow

1. Customer initiates payment
2. Validate request
3. Reserve funds (authorization)
4. Process business logic
5. Capture payment
6. Settle with bank

### Idempotency

Critical for payments:

- Same request → same result
- Use idempotency keys
- Prevent double charges on retry

### Double-Entry Bookkeeping

Every transaction has two entries:

- Debit from one account
- Credit to another account
- Total always balances

## Design: Stripe-like Payment System

### Requirements

- Process millions of transactions/day
- Support credit cards, bank transfers
- Sub-second authorization
- 99.999% availability
- PCI-DSS compliant

### Tasks

### Task 1: Payment Flow (15 min)

Design the payment flow:

**API**:

```
POST /payments
{
  "amount": 1000,
  "currency": "USD",
  "payment_method": "card_xxx",
  "idempotency_key": "unique_key_123"
}
```

**Flow**:

1. Receive request
2. Validate idempotency key
3. Create payment record (PENDING)
4. Call payment processor
5. Update status (SUCCESS/FAILED)
6. Return result

### Task 2: Data Model (10 min)

```
Payment:
  - payment_id: uuid
  - idempotency_key: string (unique)
  - amount: decimal
  - currency: string
  - status: pending|processing|success|failed
  - created_at: timestamp

Ledger:
  - entry_id: uuid
  - payment_id: uuid
  - account_id: uuid
  - type: debit|credit
  - amount: decimal
  - balance_after: decimal
```

### Task 3: Failure Handling (10 min)

**Scenarios and handling**:

| Failure Point              | Detection | Recovery |
| -------------------------- | --------- | -------- |
| Before auth                |           |          |
| During auth                |           |          |
| After auth, before capture |           |          |
| Network timeout            |           |          |

**Reconciliation**:

- Daily batch to match records
- Flag mismatches for review

### Task 4: Security (10 min)

**Requirements**:

- Encrypt card data (PCI-DSS)
- Tokenization (don't store raw cards)
- Fraud detection
- Rate limiting
- Audit logs

**Architecture**:

- Card data → tokenization service
- Only tokens in main DB
- HSM for encryption keys

### Task 5: Architecture Diagram (5 min)

Draw complete architecture:

- API Gateway
- Payment Service
- Ledger Service
- Processor Adapters (Visa, Mastercard)
- Fraud Service
- Notification Service

## Output Requirements

- [ ] Payment flow designed
- [ ] Data model with ledger
- [ ] Failure handling defined
- [ ] Security measures documented
- [ ] Architecture drawn

## Success Criteria

- [ ] Understand payment flow
- [ ] Know idempotency importance
- [ ] Can design for failures
- [ ] Understand security requirements

## Next Steps

Tomorrow: **Day 25 - Design: Amazon/E-commerce** - Inventory and ordering

## Social Post Template

"Day 24/31 System Design: Payment System! Idempotency is CRITICAL. Double-entry ledger, PCI-DSS compliance, failure handling. Money doesn't tolerate bugs! #SystemDesign #Payments"

## Notes

_Your personal observations go here._

---
