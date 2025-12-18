# Day 5: Database Fundamentals - SQL vs NoSQL

## Overview

**Topic**: Choosing the right database for your system
**Estimated Time**: 60 minutes
**Difficulty**: Beginner

## Prerequisites

- Days 1-4 completed
- Basic SQL knowledge
- Understanding of data modeling

## Time Breakdown

- **Learn (20 min)**: Database concepts
- **Practice (30 min)**: Database selection exercises
- **Reflect (10 min)**: Trade-off analysis

## Database Concepts

### SQL (Relational) Databases

Examples: PostgreSQL, MySQL, Oracle

**Characteristics**:

- Structured schema (tables, rows, columns)
- ACID transactions
- Joins for relationships
- Strong consistency

**Best for**:

- Complex queries
- Transactions (banking, e-commerce)
- Structured data
- Strong relationships

### NoSQL Databases

**Document Stores** (MongoDB, CouchDB):

- JSON-like documents
- Flexible schema
- Good for: Content management, catalogs

**Key-Value Stores** (Redis, DynamoDB):

- Simple key → value mapping
- Extremely fast
- Good for: Caching, sessions, real-time data

**Wide-Column Stores** (Cassandra, HBase):

- Rows with dynamic columns
- High write throughput
- Good for: Time-series, IoT, logs

**Graph Databases** (Neo4j, Neptune):

- Nodes and relationships
- Optimized for connections
- Good for: Social networks, recommendations

### CAP Theorem

You can only guarantee 2 of 3:

- **C**onsistency: All nodes see same data
- **A**vailability: Every request gets response
- **P**artition tolerance: System works despite network failures

In distributed systems, P is required, so choose between:

- **CP**: Consistency over availability (banking)
- **AP**: Availability over consistency (social media)

### ACID vs BASE

**ACID** (SQL):

- Atomicity, Consistency, Isolation, Durability
- Strong guarantees, lower throughput

**BASE** (NoSQL):

- Basically Available, Soft state, Eventually consistent
- Higher availability, eventual consistency

## Tasks

### Task 1: Database Selection (15 min)

Choose SQL or NoSQL (and which type) for each:

**Scenario 1**: Banking transaction system

- Choice: ******\_\_\_******
- Reasoning: ******\_\_\_******

**Scenario 2**: Social media user posts

- Choice: ******\_\_\_******
- Reasoning: ******\_\_\_******

**Scenario 3**: Real-time gaming leaderboard

- Choice: ******\_\_\_******
- Reasoning: ******\_\_\_******

**Scenario 4**: Product catalog with varying attributes

- Choice: ******\_\_\_******
- Reasoning: ******\_\_\_******

**Scenario 5**: Friend connections and recommendations

- Choice: ******\_\_\_******
- Reasoning: ******\_\_\_******

### Task 2: URL Shortener Database Design (15 min)

**Schema Design**:

```
Table/Collection: _______________
Fields:
- _______________
- _______________
- _______________
```

**Database choice**: ******\_\_\_******

**Why this choice**:

- ***

**Indexes needed**:

- ***

### Task 3: CAP Analysis (10 min)

For your URL shortener:

- Is consistency or availability more important?
- What happens during network partition?
- What's acceptable: stale data or errors?

**Your analysis**:

---

### Task 4: Comparison Table (10 min)

| Feature       | PostgreSQL | MongoDB | Redis | Cassandra |
| ------------- | ---------- | ------- | ----- | --------- |
| Data model    |            |         |       |           |
| Consistency   |            |         |       |           |
| Scalability   |            |         |       |           |
| Best use case |            |         |       |           |

## Output Requirements

- [ ] 5 database selections with reasoning
- [ ] URL shortener schema designed
- [ ] CAP analysis completed
- [ ] Database comparison table filled

## Validation

- Can you explain when to use SQL vs NoSQL?
- Do you understand CAP theorem?
- Can you design appropriate schema?

## Success Criteria

- [ ] Understand SQL vs NoSQL trade-offs
- [ ] Know different NoSQL types
- [ ] Understand CAP theorem
- [ ] Can select appropriate database

## Common Pitfalls

- **Always choosing familiar**: Pick based on requirements
- **Ignoring scale needs**: Some DBs don't scale horizontally
- **Over-normalizing**: Denormalization helps performance
- **Forgetting indexes**: Queries without indexes are slow

## Next Steps

Tomorrow: **Day 6 - Database Scaling** - Replication and sharding

## Social Post Template

"Day 5/31 System Design: SQL vs NoSQL deep dive. Document, Key-Value, Wide-Column, Graph - each has its place. Learned CAP theorem: pick 2 of 3. #SystemDesign #Databases"

## Notes

_Your personal observations and diagrams go here._

---
