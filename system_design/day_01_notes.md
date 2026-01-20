## Day 1 – System Design Fundamentals: Notes

### 1. Main goal of system design

The main goal of system design is to define an architecture and set of components that **meet the product requirements reliably at current and future scale**.

- **Satisfy functional requirements**: The system must do what users need (features, correctness).
- **Handle scale and growth**: It should keep working as users, data, and traffic grow by orders of magnitude.
- **Balance trade-offs**: Make conscious choices between latency, availability, consistency, cost, complexity, etc.
- **Create a clear blueprint**: So engineers can implement, operate, and evolve the system over time.

### 2. What does "thinking at scale" mean?

"Thinking at scale" means **designing with large numbers in mind from the beginning**, not just for a small prototype.

- Consider **how things change from 100 → 1M → 100M users**.
- Use order-of-magnitude **estimations** (requests/sec, data growth, storage over years).
- Respect **latency numbers** (RAM vs SSD vs network) when placing data and services.
- Expect **failures and hotspots**: nodes will go down, one database or service can become a bottleneck.

Instead of asking only "Will this work?", you also ask "**Will this still work x1000 bigger?** If not, what breaks first?".

### 3. The RESHADED framework

RESHADED is a checklist to structure system design discussions:

1. **R – Requirements**: Clarify functional and non-functional requirements.
2. **E – Estimations**: Rough numbers for users, QPS, data size, growth, traffic patterns.
3. **S – Storage schema**: Data model, indexes, SQL vs NoSQL, how data is partitioned and replicated.
4. **H – High-level design**: Major components and how they interact (clients, APIs, services, DBs, caches).
5. **A – API design**: External and internal APIs, request/response shapes, main operations.
6. **D – Detailed design**: Go deep on critical pieces (e.g., ID generation, caching, consistency model).
7. **E – Evaluate**: Identify bottlenecks, single points of failure, and trade-offs.
8. **D – Distinctive**: What optimizations or choices make this design stand out (e.g., special caching, cost focus, analytics)?

It keeps you from jumping straight to tech buzzwords and forces you to cover the fundamentals.

---

### 4. URL Shortener using RESHADED

#### R – Requirements

- **Functional**:
  - Shorten a long URL and return a short code.
  - Redirect from short code to original long URL.
  - (Nice-to-have) Track basic click metrics (count, last accessed).
- **Non-functional**:
  - **Low latency**: Redirects should feel instant for users (~tens of ms in DC).
  - **High availability**: Redirect should almost always work, even if some machines fail.
  - **Scalable**: Handle high read traffic (many redirects) and continuous URL creation.

#### E – Estimations

- **100M new URLs / month** → ~3.3M / day → ~38 URLs / second on average.
- **10:1 read:write ratio**:
  - Writes: ~40 requests/sec (create short URL).
  - Reads: ~400 requests/sec (redirects) on average; peak could be 10–20x higher.
- **Storage for 5 years**:
  - 100M URLs/month × 12 months/year × 5 years ≈ **6 billion URLs**.
  - Assume ~150 bytes per record (short code, original URL, timestamps, metadata).
  - 6B × 150B ≈ 900B bytes ≈ **~0.9 TB** of logical data (before replication and indexes).

These are rough numbers, but enough to guide technology choices.

#### S – Storage schema

Core record (logical view):

- `short_code` (primary key, e.g., base62 string)
- `original_url` (text)
- `created_at`
- `expires_at` (optional)
- `owner_id` (optional, for logged-in users)
- `click_count` (optional, can also be offloaded to analytics store)

Storage options:

- **Primary mapping** short_code → original_url in a **key-value store** (NoSQL or cache + persistent store) for very fast lookups.
- For analytics and user features, you can use an additional store (SQL or OLAP) but keep redirect path as simple and fast as possible.

#### H – High-level design

- **Clients** (browser / mobile apps) call the service.
- **Load balancer** routes traffic to multiple **application servers**.
- App servers:
  - Expose APIs for shortening and redirecting.
  - Talk to a **cache** (e.g., Redis) to get short_code → URL quickly.
  - Fall back to a **persistent datastore** (e.g., key-value DB or relational DB) on cache miss.
- Optional **background workers** to aggregate click logs into analytics storage.

Redirect flow: client → LB → app server → cache → DB (if needed) → 301/302 redirect.

#### A – API design (examples)

- `POST /shorten`
  - Request: `{ "long_url": "https://example.com/very/long/..." }`
  - Response: `{ "short_url": "https://sho.rt/abc123" }`
- `GET /{code}`
  - Request: `GET /abc123`
  - Behavior: Look up `abc123`, redirect to stored `original_url` with HTTP 301/302.

Internal APIs can exist between services (e.g., analytics, admin), but the core is minimal.

#### D – Detailed design (critical pieces)

- **ID/short code generation**:
  - Use a unique numeric ID (from DB auto-increment or ID service) and encode in **base62** to get a short alphanumeric code.
  - Or use a random generator with collision checks in the DB.
- **Caching strategy**:
  - On redirect, first check cache; if miss, read from DB, then populate cache.
  - Use TTL to keep cache fresh and bound memory.
- **Scalability**:
  - Horizontally scale app servers behind the load balancer.
  - Shard or partition data store by short_code range or hash if a single DB becomes a bottleneck.
- **Reliability**:
  - Replicate the database (primary + replicas) to survive node failures.
  - Health checks and automatic failover where possible.

#### E – Evaluate

- **Bottlenecks**:
  - Database hot spots if many reads hit the same partition → mitigated with caching and good key distribution.
  - Single-region deployment increases latency for users far away → multi-region deployment later.
- **Trade-offs**:
  - Strong consistency on redirects (always read latest URL) vs allowing brief staleness with heavy caching.
  - Simpler single DB vs sharded/replicated setup.

#### D – Distinctive

- Heavier use of **caching** to handle read-heavy workload efficiently.
- Built-in **analytics** (click counts, geo stats) via logs and offline processing.
- Support for **custom domains** and branded links as a product differentiator.

---

### 5. Key Learnings

- Start every design with **requirements and scale assumptions**, not with databases or buzzwords.
- Simple **back-of-the-envelope estimates** quickly reveal storage and throughput needs.
- The **RESHADED framework** keeps the conversation structured and reduces the chance of missing critical aspects.
- **Latency numbers** matter when deciding where to put computation and data (memory vs disk vs network).
- Designs should explicitly think about **failure, replication, and growth**, even for simple systems like a URL shortener.

---

### 6. Checklist

- [x] Understand scale mindset
- [x] Know key latency numbers (at least approximate orders of magnitude)
- [x] Applied framework to simple problem (URL shortener)
- [x] Ready for deeper concepts (caching strategies, replication, consistency models)

---

### 7. Common Mistakes and How to Avoid Them

- **Jumping to solutions**
  - Mistake: Immediately saying "We’ll use Kafka, Redis, and microservices" without understanding what’s needed.
  - Avoid it: Always start with **R – Requirements** and write them down before picking tools.

- **Ignoring scale**
  - Mistake: Designing only for current traffic (e.g., 100 users) and being surprised when things break at 1M users.
  - Avoid it: Do quick **E – Estimations** (QPS, data size, growth) and ask how the design behaves when numbers 10x–100x.

- **Forgetting non-functional requirements**
  - Mistake: Only thinking about "does it work" and ignoring latency, availability, and reliability.
  - Avoid it: Explicitly list **non-functional requirements** (latency SLOs, uptime targets) early and check design against them.

- **Not estimating**
  - Mistake: Hand-wavy answers like "we’ll just store it in a database" without knowing if it fits or how fast it must be.
  - Avoid it: Do **back-of-envelope math** for storage and throughput, using the latency and size numbers from the cheat sheet.

These notes should help guide future designs and serve as a reference when practicing more complex systems.
