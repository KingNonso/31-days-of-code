# Day 20: Design Ride-Sharing (Uber/Lyft)

## Overview

**Topic**: Location-based services at scale
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 19 completed
- Understanding of geospatial queries
- Real-time systems knowledge

## Time Breakdown

- **Learn (20 min)**: Location-based concepts
- **Design (30 min)**: Complete system
- **Reflect (10 min)**: Real-time challenges

## Location-Based Concepts

### Geospatial Indexing

**Geohash**:

- Encode lat/long into string
- Nearby locations share prefix
- "9q8yy" → San Francisco area

**Quadtree**:

- Divide space into quadrants
- Subdivide based on density
- Efficient for varying density

**S2/H3**:

- Sphere divided into cells
- Hierarchical levels
- Used by Uber (H3)

### Matching Algorithm

1. Rider requests ride
2. Find nearby available drivers
3. Rank by distance, rating, ETA
4. Send to best match
5. Driver accepts/rejects

## Design: Uber-Scale Ride Sharing

### Requirements

- 100M monthly active users
- 5M drivers
- 20M trips/day
- Match in <10 seconds
- Real-time location updates

### Tasks

### Task 1: Location Service (10 min)

**Driver location updates**:

- Frequency: Every 3 seconds
- Data: {driver_id, lat, long, status, timestamp}

**Storage**:

```
5M drivers × updates every 3 sec = 1.7M updates/sec
```

**How to store**:

- In-memory: ******\_\_\_******
- Database: ******\_\_\_******
- Index: ******\_\_\_******

### Task 2: Matching Service (15 min)

**Matching flow**:

1. Rider requests at location (lat, long)
2. Query nearby drivers (radius or k-nearest)
3. Filter: available, car type, rating
4. Rank: ETA, rating, acceptance rate
5. Send request to top driver
6. Timeout → next driver

**Query design**:

```
Find drivers where:
  - distance(driver, rider) < 5 km
  - status = available
  - car_type in [requested_types]
ORDER BY ETA
LIMIT 10
```

### Task 3: Trip Service (10 min)

**Trip lifecycle**:

1. REQUESTED
2. MATCHED
3. DRIVER_EN_ROUTE
4. ARRIVED
5. IN_PROGRESS
6. COMPLETED

**State machine design**:

- Valid transitions
- Actions on each transition
- Timeout handling

### Task 4: ETA Calculation (10 min)

**Factors**:

- Distance (crow fly vs road)
- Traffic conditions
- Historical patterns
- Time of day

**Architecture**:

- Maps service (routing)
- Traffic service (real-time)
- ML model (prediction)

### Task 5: Architecture Diagram (5 min)

Draw showing:

- Mobile apps (rider, driver)
- API Gateway
- Location Service
- Matching Service
- Trip Service
- Payment Service
- Notification Service

## Output Requirements

- [ ] Location storage designed
- [ ] Matching algorithm defined
- [ ] Trip state machine designed
- [ ] ETA calculation approach
- [ ] Architecture drawn

## Success Criteria

- [ ] Understand geospatial indexing
- [ ] Can design real-time location system
- [ ] Know matching algorithm
- [ ] Can handle millions of location updates

## Next Steps

Tomorrow: **Day 21 - Week 3 Review** - Design Web Crawler

## Social Post Template

"Day 20/31 System Design: Uber/Lyft! Geohash for location, 1.7M updates/sec, match in <10 sec. Real-time location at scale is HARD. #SystemDesign #LocationBased"

## Notes

_Your personal observations go here._

---
