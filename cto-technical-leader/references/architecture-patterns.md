# Technical Architecture Patterns & Decisions

## System Architecture Evolution

### Stage 1: Monolith (0-20 engineers)
**Characteristics**:
- Single deployable unit
- Shared database
- Simple deployment pipeline
- All code in one repository

**When It Works**:
- Small team, fast iteration
- Domain boundaries unclear
- Limited operational expertise
- Speed to market priority

**Warning Signs to Evolve**:
- Deployments take hours
- Teams stepping on each other
- Can't scale different components independently
- Test suite takes >30 minutes

---

### Stage 2: Modular Monolith (20-50 engineers)
**Characteristics**:
- Clear module boundaries within monolith
- Internal APIs between modules
- Shared database with schema ownership
- Potential for future extraction

**Benefits**:
- Maintains deployment simplicity
- Enforces domain boundaries
- Easier refactoring within modules
- Foundation for microservices if needed

**Implementation**:
- Define module interfaces explicitly
- Enforce dependency rules (no circular deps)
- Database schema prefixes per module
- Consider separate test suites per module

---

### Stage 3: Service-Oriented Architecture (50-150 engineers)
**Characteristics**:
- 5-15 services around domain boundaries
- Services own their data
- API contracts between services
- Independent deployment possible

**Key Services Typically Extracted**:
- User/Identity service
- Payment/Billing service
- Notification service
- Search service
- Analytics/Data pipeline

**Prerequisites**:
- Strong CI/CD pipeline
- Observability infrastructure
- Service discovery mechanism
- API versioning strategy

---

### Stage 4: Microservices (150+ engineers)
**Characteristics**:
- Many small, focused services
- Team ownership per service
- Polyglot technology stack possible
- Complex operational requirements

**When Justified**:
- Very large organization
- Distinct scaling requirements
- Teams need full autonomy
- Mature operational capabilities

**Hidden Costs**:
- Distributed system complexity
- Network latency overhead
- Data consistency challenges
- Operational tooling requirements
- Debugging difficulty

---

## API Design Patterns

### REST API Guidelines

**Resource Naming**:
- Use nouns, not verbs: `/users`, not `/getUsers`
- Plural for collections: `/orders`, `/products`
- Hierarchical relationships: `/users/{id}/orders`
- Use kebab-case: `/order-items`, not `/orderItems`

**HTTP Methods**:
| Method | Purpose | Idempotent |
|--------|---------|------------|
| GET | Read resource | Yes |
| POST | Create resource | No |
| PUT | Replace resource | Yes |
| PATCH | Update resource | No |
| DELETE | Remove resource | Yes |

**Status Codes**:
- 200: Success
- 201: Created
- 204: No Content (successful DELETE)
- 400: Bad Request (client error)
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 409: Conflict
- 422: Unprocessable Entity (validation)
- 500: Internal Server Error

**Versioning**:
- URL path: `/v1/users` (preferred)
- Header: `Accept: application/vnd.api+json;version=1`
- Query param: `/users?version=1`

---

### GraphQL Considerations

**When to Use**:
- Complex, nested data requirements
- Mobile apps with bandwidth constraints
- Rapidly evolving frontend needs
- Multiple client types with different data needs

**When to Avoid**:
- Simple CRUD operations
- File uploads as primary use case
- Team unfamiliar with GraphQL
- Caching requirements are complex

**Best Practices**:
- Schema-first design
- Pagination with cursors
- Rate limiting by query complexity
- Persisted queries for production

---

### gRPC Considerations

**When to Use**:
- Internal service-to-service communication
- High performance requirements
- Strong typing with code generation
- Streaming requirements

**When to Avoid**:
- Browser clients (without proxy)
- Public APIs
- Simple integrations
- Team unfamiliar with Protocol Buffers

---

## Database Selection

### Relational (PostgreSQL, MySQL)

**Use When**:
- Complex queries and joins
- ACID transactions required
- Structured data with relationships
- Reporting and analytics needs
- Well-defined schema

**PostgreSQL Advantages**:
- JSON support for flexibility
- Advanced indexing (GIN, GiST)
- Extensions ecosystem
- Strong community

---

### Document Store (MongoDB, DynamoDB)

**Use When**:
- Schema flexibility needed
- Hierarchical data structures
- Read-heavy workloads
- Horizontal scaling priority
- Rapid iteration on data model

**Avoid When**:
- Complex transactions across documents
- Heavy reporting needs
- Many-to-many relationships

---

### Key-Value / Cache (Redis)

**Use Cases**:
- Session storage
- Caching layer
- Rate limiting
- Real-time leaderboards
- Pub/sub messaging
- Distributed locks

**Patterns**:
- Cache-aside (application manages cache)
- Write-through (cache updated on write)
- TTL-based expiration
- Cache invalidation strategies

---

### Search (Elasticsearch)

**Use When**:
- Full-text search
- Faceted filtering
- Log aggregation
- Analytics on unstructured data

**Considerations**:
- Not a primary database
- Eventual consistency
- Resource intensive
- Complex operations management

---

### Time Series (InfluxDB, TimescaleDB)

**Use When**:
- Metrics and monitoring
- IoT sensor data
- Financial tick data
- Event logging with time-based queries

---

## Event-Driven Architecture

### Message Queues (SQS, RabbitMQ)

**Patterns**:
- Point-to-point: One producer, one consumer
- Work queue: Multiple workers processing jobs
- Fan-out: One message to multiple consumers

**Use Cases**:
- Async task processing
- Decoupling services
- Load leveling
- Retry handling

---

### Event Streaming (Kafka)

**Patterns**:
- Event sourcing: Store state as event sequence
- CQRS: Separate read and write models
- Change data capture: Database change streaming

**Use Cases**:
- Real-time data pipelines
- Audit logs
- Cross-service data sync
- Analytics event collection

**Considerations**:
- Operational complexity
- Message ordering guarantees
- Consumer group management
- Schema evolution strategy

---

## Infrastructure Patterns

### Container Orchestration (Kubernetes)

**When to Adopt**:
- Multiple services to manage
- Need for auto-scaling
- Complex deployment requirements
- Team has operational expertise

**When to Avoid**:
- Small team, simple infrastructure
- Single application
- No Kubernetes expertise
- Managed alternatives sufficient (ECS, Cloud Run)

---

### Serverless (Lambda, Cloud Functions)

**Ideal For**:
- Event-driven workloads
- Sporadic traffic patterns
- Simple, stateless functions
- Rapid prototyping

**Limitations**:
- Cold start latency
- Execution time limits
- State management complexity
- Debugging difficulty
- Potential vendor lock-in

---

### Edge Computing (CloudFlare Workers, Lambda@Edge)

**Use Cases**:
- Latency-sensitive operations
- Request routing and manipulation
- A/B testing at edge
- Personalization
- Security (WAF, bot detection)

---

## Reliability Patterns

### Circuit Breaker
- Prevent cascade failures
- Fast fail when downstream is unhealthy
- Automatic recovery testing
- Libraries: Hystrix, resilience4j, Polly

### Retry with Backoff
- Exponential backoff: 1s, 2s, 4s, 8s...
- Jitter to prevent thundering herd
- Max retry limits
- Idempotency keys for safety

### Bulkhead
- Isolate failures to prevent spread
- Thread pool or connection isolation
- Resource limits per dependency

### Rate Limiting
- Protect services from overload
- Token bucket or sliding window
- Different limits by tier/customer
- Graceful degradation responses

### Health Checks
- Liveness: Is the process running?
- Readiness: Can it handle traffic?
- Deep health: Dependencies healthy?
- Separate endpoints for each

---

## Technology Evaluation Framework

### Evaluation Criteria

| Factor | Questions to Ask |
|--------|------------------|
| Fit | Does it solve our actual problem? |
| Maturity | Production-proven at our scale? |
| Ecosystem | Community, documentation, integrations? |
| Team | Do we have or can we hire expertise? |
| Cost | Total cost of ownership over 3 years? |
| Risk | What happens if it fails or goes away? |
| Lock-in | How hard to switch if needed? |

### Proof of Concept Structure
1. Define success criteria upfront
2. Time-box evaluation (1-2 weeks)
3. Test realistic scenarios, not just happy path
4. Include operational aspects (monitoring, debugging)
5. Document findings and recommendation
6. Get team buy-in before committing
