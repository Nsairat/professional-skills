# System Design Patterns & Reference Architectures

## System Design Methodology

### Step-by-Step Approach

**Step 1: Clarify Requirements (5 min)**
- Functional requirements: What should the system do?
- Non-functional requirements: Scale, latency, availability
- Constraints: Budget, timeline, existing systems
- Out of scope: What are we NOT building?

**Step 2: Capacity Estimation (5 min)**
- Users: DAU, MAU, peak concurrent
- Traffic: Requests per second, read/write ratio
- Storage: Data per user, growth rate, retention
- Bandwidth: Request/response sizes

**Step 3: High-Level Design (10 min)**
- Core components and their responsibilities
- Data flow between components
- API design (key endpoints)
- Database choice and schema

**Step 4: Deep Dive (15 min)**
- Scale bottlenecks and solutions
- Data partitioning strategy
- Caching layers
- Failure handling

**Step 5: Wrap-Up (5 min)**
- Trade-offs made
- Future improvements
- Monitoring approach

---

## Common System Designs

### URL Shortener (TinyURL)

**Requirements**
- Shorten long URLs to short codes
- Redirect short URLs to original
- Analytics (optional)
- Scale: 100M URLs, 10:1 read/write ratio

**Architecture**
```
┌─────────┐     ┌─────────────┐     ┌──────────┐
│ Client  │────►│ API Gateway │────►│ Shortener│
└─────────┘     │ + LB        │     │ Service  │
                └─────────────┘     └────┬─────┘
                                         │
                      ┌──────────────────┼──────────────────┐
                      │                  │                  │
                 ┌────▼────┐        ┌────▼────┐       ┌─────▼────┐
                 │  Cache  │        │  MySQL  │       │  Counter │
                 │ (Redis) │        │ (URLs)  │       │ Service  │
                 └─────────┘        └─────────┘       └──────────┘
```

**Key Decisions**
- ID generation: Base62 encoding of auto-increment ID or hash
- Storage: Key-value store or relational DB
- Cache: Redis for hot URLs
- Scale: Horizontal sharding by URL hash

---

### Rate Limiter

**Requirements**
- Limit requests per user/IP/API key
- Multiple limit windows (per second, per minute)
- Distributed across multiple servers
- Low latency addition

**Algorithms**

| Algorithm | Pros | Cons |
|-----------|------|------|
| Token Bucket | Smooth, allows bursts | Memory per user |
| Leaky Bucket | Smooth output rate | Can delay requests |
| Fixed Window | Simple | Boundary burst issue |
| Sliding Window | Accurate | More complex |

**Architecture**
```
┌─────────┐     ┌─────────────┐     ┌──────────┐     ┌─────────┐
│ Client  │────►│ Rate Limiter│────►│ Backend  │────►│ Database│
└─────────┘     │ Middleware  │     │ Service  │     └─────────┘
                └──────┬──────┘     └──────────┘
                       │
                  ┌────▼────┐
                  │  Redis  │
                  │ (Counts)│
                  └─────────┘
```

**Redis Implementation (Sliding Window)**
```
Key: rate_limit:{user_id}:{window_start}
Value: request_count
TTL: window_size + buffer
```

---

### Distributed Cache

**Requirements**
- Low latency reads (<1ms)
- High availability
- Scalable to petabytes
- Eventual consistency acceptable

**Architecture**
```
┌─────────┐     ┌─────────────────────────────────────────┐
│ Client  │────►│           Cache Cluster                 │
└─────────┘     │  ┌───────┐  ┌───────┐  ┌───────┐       │
                │  │Node 1 │  │Node 2 │  │Node 3 │       │
                │  │ A-G   │  │ H-P   │  │ Q-Z   │       │
                │  └───────┘  └───────┘  └───────┘       │
                │         (Consistent Hashing)            │
                └─────────────────────────────────────────┘
                                   │
                              ┌────▼────┐
                              │ Database│
                              │ (Source)│
                              └─────────┘
```

**Key Patterns**
- Consistent hashing for distribution
- Replication for availability
- LRU/LFU eviction policies
- Write-through vs write-behind

---

### Message Queue

**Requirements**
- At-least-once delivery
- Ordering within partition
- High throughput (millions/sec)
- Retention for replay

**Architecture (Kafka-style)**
```
┌──────────┐                                    ┌──────────┐
│ Producer │──┐                            ┌───►│ Consumer │
└──────────┘  │    ┌────────────────────┐  │    │ Group A  │
              ├───►│      Topic         │──┤    └──────────┘
┌──────────┐  │    │ ┌────┐ ┌────┐ ┌────┐│  │    
│ Producer │──┤    │ │P0  │ │P1  │ │P2  ││  │    ┌──────────┐
└──────────┘  │    │ └────┘ └────┘ └────┘│  └───►│ Consumer │
              │    └────────────────────┘       │ Group B  │
┌──────────┐  │              │                  └──────────┘
│ Producer │──┘         Replication
└──────────┘                 │
                    ┌────────┴────────┐
                    │    ZooKeeper    │
                    │  (Coordination) │
                    └─────────────────┘
```

**Key Concepts**
- Topics and partitions
- Consumer groups
- Offset management
- Replication factor

---

### Search System

**Requirements**
- Full-text search
- Relevance ranking
- Faceted filtering
- Autocomplete
- Scale: Billions of documents

**Architecture**
```
┌─────────┐     ┌─────────────┐     ┌─────────────────────────────┐
│ Client  │────►│ Search API  │────►│     Search Cluster          │
└─────────┘     └─────────────┘     │  ┌───────┐  ┌───────┐      │
                                    │  │Shard 1│  │Shard 2│ ...  │
                                    │  │Primary│  │Primary│      │
                                    │  │Replica│  │Replica│      │
                                    │  └───────┘  └───────┘      │
                                    └─────────────────────────────┘
                                                  ▲
                                                  │
┌─────────────┐     ┌─────────────┐              │
│ Data Source │────►│  Indexer    │──────────────┘
└─────────────┘     └─────────────┘
```

**Key Components**
- Inverted index structure
- Tokenization and analyzers
- TF-IDF / BM25 ranking
- Sharding strategy (by document ID or time)

---

### Notification System

**Requirements**
- Multiple channels (push, email, SMS)
- Millions of notifications per day
- Delivery guarantees
- User preferences

**Architecture**
```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│ Event       │────►│ Notification│────►│   Router    │
│ Source      │     │ Service     │     │             │
└─────────────┘     └─────────────┘     └──────┬──────┘
                                               │
                    ┌──────────────────────────┼──────────────────────────┐
                    │                          │                          │
              ┌─────▼─────┐              ┌─────▼─────┐              ┌─────▼─────┐
              │   Push    │              │   Email   │              │    SMS    │
              │  Service  │              │  Service  │              │  Service  │
              └─────┬─────┘              └─────┬─────┘              └─────┬─────┘
                    │                          │                          │
              ┌─────▼─────┐              ┌─────▼─────┐              ┌─────▼─────┐
              │   APNS/   │              │ SendGrid/ │              │  Twilio/  │
              │    FCM    │              │   SES     │              │   Plivo   │
              └───────────┘              └───────────┘              └───────────┘
```

**Key Considerations**
- Rate limiting per channel
- Retry with exponential backoff
- User preference management
- Deduplication
- Analytics and tracking

---

### Content Delivery Network (CDN)

**Requirements**
- Global content distribution
- Low latency (<50ms)
- High cache hit ratio (>95%)
- Origin protection

**Architecture**
```
                         ┌─────────────────────────────────┐
                         │         CDN Edge Layer          │
                         │  ┌─────┐ ┌─────┐ ┌─────┐       │
                         │  │PoP 1│ │PoP 2│ │PoP N│       │
                         │  │US-E │ │EU-W │ │APAC │       │
                         │  └──┬──┘ └──┬──┘ └──┬──┘       │
                         └─────┼───────┼───────┼──────────┘
                               │       │       │
Users ─────────────────────────┴───────┴───────┘
                                       │
                                  (Cache Miss)
                                       │
                               ┌───────▼───────┐
                               │  Origin       │
                               │  Shield       │
                               └───────┬───────┘
                                       │
                               ┌───────▼───────┐
                               │    Origin     │
                               │    Server     │
                               └───────────────┘
```

**Caching Strategies**
- Cache-Control headers
- Stale-while-revalidate
- Cache invalidation (purge, versioned URLs)
- Edge compute for personalization

---

### Payment System

**Requirements**
- PCI compliance
- Multiple payment methods
- Idempotency
- Reconciliation

**Architecture**
```
┌─────────┐     ┌─────────────┐     ┌─────────────┐
│ Client  │────►│  Payment    │────►│  Payment    │
│         │     │  Gateway    │     │  Processor  │
└─────────┘     └──────┬──────┘     └──────┬──────┘
                       │                    │
                  ┌────▼────┐          ┌────▼────┐
                  │ Ledger  │          │ External│
                  │ Service │          │ Provider│
                  └────┬────┘          │(Stripe) │
                       │               └─────────┘
                  ┌────▼────┐
                  │ Database│
                  │ (Txns)  │
                  └─────────┘
```

**Key Patterns**
- Idempotency keys for duplicate prevention
- Two-phase commit or saga for distributed transactions
- Event sourcing for audit trail
- Reconciliation batch jobs

---

## Scalability Cheat Sheet

### Numbers Every Architect Should Know

| Operation | Latency |
|-----------|---------|
| L1 cache reference | 0.5 ns |
| L2 cache reference | 7 ns |
| RAM reference | 100 ns |
| SSD random read | 150 μs |
| HDD random read | 10 ms |
| Network round trip (same datacenter) | 0.5 ms |
| Network round trip (cross-region) | 100 ms |

### Capacity Estimation

| Time | Seconds |
|------|---------|
| 1 day | 86,400 |
| 1 month | 2.5M |
| 1 year | 31.5M |

| Data | Bytes |
|------|-------|
| 1 KB | 1,000 |
| 1 MB | 1,000,000 |
| 1 GB | 1,000,000,000 |
| 1 TB | 1,000,000,000,000 |

### Quick Math

**Requests per second:**
- 1M daily active users
- 10 requests per user per day
- = 10M requests / 86,400 seconds
- ≈ 115 RPS average
- ≈ 350 RPS peak (3x average)

**Storage:**
- 1M users
- 1 KB per user
- = 1 GB total
- Growth: 10% monthly = 3 GB in 1 year

---

## Anti-Patterns to Avoid

### Distributed Monolith
- Microservices with tight coupling
- Synchronous calls between all services
- Shared database between services
- Solution: True service boundaries, async communication

### Premature Optimization
- Building for 1M users when you have 1K
- Complex caching before needed
- Microservices with small team
- Solution: Start simple, measure, optimize

### Insufficient Redundancy
- Single points of failure
- No disaster recovery plan
- Untested backups
- Solution: N+1 redundancy, regular DR testing

### Over-Engineering
- Too many abstraction layers
- Unnecessary flexibility
- Gold-plating
- Solution: YAGNI, solve today's problems

### Ignoring Operations
- No monitoring or alerting
- Manual deployments
- No runbooks
- Solution: DevOps from day one
