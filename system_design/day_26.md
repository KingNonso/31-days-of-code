# Day 26: Design Monitoring System

## Overview

**Topic**: Observability and monitoring at scale
**Estimated Time**: 60 minutes
**Difficulty**: Advanced

## Prerequisites

- Day 25 completed
- Understanding of metrics and logs
- Basic time-series concepts

## Time Breakdown

- **Learn (20 min)**: Monitoring concepts
- **Design (30 min)**: Complete system
- **Reflect (10 min)**: Alert design

## Monitoring Concepts

### Three Pillars of Observability

**Metrics**:

- Numeric measurements over time
- CPU, memory, request count, latency
- Aggregatable, low cardinality

**Logs**:

- Discrete events with context
- Request details, errors, debug info
- High cardinality, searchable

**Traces**:

- Request flow across services
- Latency breakdown
- Distributed debugging

### Metrics Types

- **Counter**: Only increases (requests, errors)
- **Gauge**: Can increase/decrease (CPU, memory)
- **Histogram**: Distribution (latency percentiles)

### Time-Series Database

- Optimized for time-based queries
- High write throughput
- Efficient compression
- Examples: Prometheus, InfluxDB, TimescaleDB

## Design: Datadog-like Monitoring System

### Requirements

- 1M+ hosts sending metrics
- 10M metrics/second ingestion
- Sub-minute query latency
- 13-month retention
- Real-time alerting

### Tasks

### Task 1: Data Collection (10 min)

**Agent design**:

- Runs on each host
- Collects system metrics
- Supports custom metrics
- Batches and sends to collector

**Data format**:

```
{
  "metric": "cpu.usage",
  "value": 75.5,
  "timestamp": 1642000000,
  "tags": {
    "host": "web-01",
    "env": "production"
  }
}
```

### Task 2: Ingestion Pipeline (10 min)

**Architecture**:

1. **Collector**: Receive from agents
2. **Kafka**: Buffer and distribute
3. **Processor**: Aggregate, downsample
4. **Storage**: Time-series DB

**Write path**:

- Batch writes (efficiency)
- Pre-aggregate common queries
- Downsample old data (1min → 5min → 1hr)

### Task 3: Storage Design (10 min)

**Schema**:

```
Metric:
  - metric_name: string
  - tags: map<string, string>
  - timestamp: int64
  - value: float64
```

**Partitioning**:

- By time (daily/weekly chunks)
- By metric name
- Hot/warm/cold tiers

**Compression**:

- Delta encoding for timestamps
- Gorilla compression for values
- 10-20x compression typical

### Task 4: Query Engine (10 min)

**Query types**:

- Point query: value at specific time
- Range query: values over time range
- Aggregation: avg, max, percentiles

**Query language** (PromQL-like):

```
avg(cpu.usage{env="production"}) by (host)
rate(http_requests_total[5m])
histogram_quantile(0.99, http_latency)
```

### Task 5: Alerting (10 min)

**Alert definition**:

```yaml
alert: HighCPU
expr: cpu.usage > 90
for: 5m
labels:
  severity: critical
annotations:
  summary: "CPU usage above 90%"
```

**Alert pipeline**:

1. Evaluate rules periodically
2. Check threshold
3. Deduplicate
4. Route to channels (email, Slack, PagerDuty)

## Output Requirements

- [ ] Agent and data format designed
- [ ] Ingestion pipeline architected
- [ ] Storage with compression
- [ ] Query engine designed
- [ ] Alerting system defined

## Success Criteria

- [ ] Understand three pillars
- [ ] Can design metrics pipeline
- [ ] Know time-series storage
- [ ] Can design alerting

## Next Steps

Tomorrow: **Day 27 - Design: Distributed ID Generator** - Unique IDs at scale

## Social Post Template

"Day 26/31 System Design: Monitoring System! Metrics, logs, traces - the three pillars. 10M metrics/sec ingestion, time-series storage, real-time alerting. Observability FTW! #SystemDesign #Monitoring"

## Notes

_Your personal observations go here._

---
