# Day 1: System Design Fundamentals - Thinking at Scale

## Overview

**Topic**: Introduction to system design thinking and scalability concepts
**Estimated Time**: 60 minutes
**Difficulty**: Beginner

## Prerequisites

- Basic understanding of web applications
- Familiarity with client-server architecture
- Notebook for diagrams

## Time Breakdown

- **Learn (25 min)**: Core concepts and video
- **Practice (25 min)**: Apply framework to simple system
- **Reflect (10 min)**: Document key learnings

## Core Concepts

### What is System Design?

System design is the process of defining architecture, components, and data flow to satisfy requirements at scale.

### The Scale Mindset

Think in terms of:

- **Users**: 1 → 1,000 → 1,000,000 → 1,000,000,000
- **Data**: MB → GB → TB → PB
- **Requests**: 1/sec → 1,000/sec → 1,000,000/sec

### Key Metrics to Consider

- **Latency**: How fast is the response?
- **Throughput**: How many requests per second?
- **Availability**: What % of time is system up?
- **Consistency**: Is data the same everywhere?

### The System Design Framework (RESHADED)

1. **R**equirements: What are we building?
2. **E**stimations: How big? How fast?
3. **S**torage schema: What data? How stored?
4. **H**igh-level design: Major components
5. **A**PI design: How do components talk?
6. **D**etailed design: Deep dive on key parts
7. **E**valuate: Trade-offs and bottlenecks
8. **D**istinctive: What makes this unique?

## Resources

- [System Design Primer - GitHub](https://github.com/donnemartin/system-design-primer)
- [Gaurav Sen - System Design Introduction](https://www.youtube.com/watch?v=xpDnVSmNFX0) (15 min)

## Tasks

### Task 1: Watch Introduction Video (15 min)

Watch the Gaurav Sen video. Take notes on:

- Why system design matters
- Key concepts introduced
- Questions you have

### Task 2: Learn the Numbers (10 min)

Memorize these critical numbers:

| Operation                            | Time   |
| ------------------------------------ | ------ |
| L1 cache reference                   | 0.5 ns |
| L2 cache reference                   | 7 ns   |
| RAM reference                        | 100 ns |
| SSD random read                      | 150 μs |
| HDD seek                             | 10 ms  |
| Network round trip (same datacenter) | 500 μs |
| Network round trip (cross-continent) | 150 ms |

### Task 3: Apply Framework to URL Shortener (25 min)

Design a simple URL shortener using RESHADED:

**R - Requirements**:

- Functional: Shorten URL, redirect to original
- Non-functional: Low latency, high availability

**E - Estimations**:

- 100M URLs created/month
- 10:1 read:write ratio
- Storage needed for 5 years?

**S - Storage**:

- What fields needed?
- SQL or NoSQL?

**H - High-level design**:

- Draw basic architecture (client, server, database)

### Task 4: Document Key Learnings (10 min)

Write answers to:

1. What is the main goal of system design?
2. What does "thinking at scale" mean?
3. What is the RESHADED framework?

## Output Requirements

- [ ] Video watched with notes
- [ ] Critical numbers memorized (or noted)
- [ ] URL shortener basic design sketched
- [ ] Key learnings documented

## Validation

- Can you explain why system design matters?
- Do you understand the RESHADED framework?
- Can you estimate storage for a simple system?

## Success Criteria

- [ ] Understand scale mindset
- [ ] Know key latency numbers
- [ ] Applied framework to simple problem
- [ ] Ready for deeper concepts

## Common Pitfalls

- **Jumping to solutions**: Always clarify requirements first
- **Ignoring scale**: 100 users ≠ 100 million users
- **Forgetting non-functional requirements**: Availability, latency matter
- **Not estimating**: Back-of-envelope math is essential

## Next Steps

Tomorrow: **Day 2 - Horizontal vs Vertical Scaling** - How to handle growth

## Social Post Template

"Day 1/31 System Design: Learned the RESHADED framework and scale mindset. Designed a basic URL shortener. Key insight: always start with requirements. #SystemDesign #31DayChallenge"

## Notes

_Your personal observations and diagrams go here._

---
